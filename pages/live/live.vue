<template>
	<view>
	<!-- <live-pusher  id='livePusher' ref="livePusher" class="back_img" url="https://domain/push_stream"
	 	mode="SD" :muted="true" :enable-camera="true" :auto-focus="true" :beauty="1" whiteness="2"
	 	aspect="9:16" @statechange="statechange" @netstatus="netstatus" 
	 	></live-pusher> -->

		<image class="back_img" :style="fullHeight"
		src="/static/backimg.jpg" ></image>
		<view class="player_view">
			<!-- 顶部信息 -->
			<view class="tp_user">
				<image src="" mode=""></image>
				<view class="content">
					<view class="text">星狐集团</view>
					<view class="text" style="font-size:22rpx">1300人观看</view>
				</view>
				<view class="follow" v-if="uPop" @click="cancel_follow">取关</view>
				<view class="follow" v-else @click="follow">关注</view>
			</view>
			<!-- 点赞数 -->
			<view class="zan_view">
				<image src="/static/love.png" mode=""></image>
				<view>666点赞</view>
			</view>
			<!-- 房间号 -->
			<view class="home_id_view">
				<image src="/static/home_name.png" mode=""></image>
				<view>ID:0001</view>
			</view>
			<!-- 弹窗提示 -->
			<!-- <view class="pop_view" v-if="pop">
				<image src="/static/tip_shop.png" mode=""></image>
				<image v-if="pop_follw" src="/static/tip_follow.png" mode=""></image>
			</view> -->
			<!-- 平台提示 -->
			<view class="tips_view">
				平台依法对直播内容进行24小时巡查,倡
				导绿色直播,维护网络文明健康。切勿与他
				人私下交易,非官方活动谨慎参与,避免上
				当受骗。                     
			</view>
			<scroll-view class="comment_list" scroll-y="true" 
			show-scrollbar="false"
			:scroll-top='scrolTop' >
				<!-- <view class="com_item" v-for="(item,index) in com_list" :key="item.index">
					<view class="com_name">
						吃货大王呀：
					</view>
					<view class="com_content">{{item}}</view>
				</view> -->
			</scroll-view>
			<!-- <view  >
				
				
			</view> -->
			<!-- <view class="comment">
				<input type="text" 
				:value="com_text" 
				placeholder="说点什么..." 
				placeholder-style="font-size:26rpx;color:white" 
				confirm-type="send"
			
				@confirm="send"
				@input="comment_text" />
			</view> -->
			<view class="bottom_btn">
				<view class="btn_view">
					<image src="/static/chu.png" mode=""></image>
					<view>橱窗</view>
				</view>
				<view class="btn_view">
					<image src="/static/more.png" mode=""></image>
					<view>更多</view>
				</view>
				<view class="btn_view">
					<image src="/static/gift.png" mode=""></image>
					<view>礼物</view>
				</view>
				<view class="btn_view" @click="zan">
					<image src="/static/zan.png" mode=""></image>
					<view>点赞</view>
				</view>
			</view>
			
		</view>
		
	</view>
</template>

<script>
	export default {
	
		data() {
			return {
				fil: true,
				uPop:false,
				pop:false,
				pop_follw:true,
				pop_time:0,
				fullHeight:0,
				com_text:'',
				com_list:['多少钱?'],
				doms:'',
				scrolTop:500
			};
		},
		onLoad() {
			uni.getSystemInfo({
				success: (res)=> {
					this.fullHeight ="height:" + res.windowHeight + "px";
					console.log(this.fullHeight);
				}
			})
			
			console.log('')
			this.pop = true
			this.pop_follw = true
			this.pop_setInt()
		},
		onReady() {
				// 注意：需要在onReady中 或 onLoad 延时
				this.context = uni.createLivePusherContext("livePusher", this);
		},
		methods:{
			start: function() {
							 console.log('开始推流',this.context)
							 this.context.start({
								 success: (a) => {
									 console.log("livePusher.start:" + JSON.stringify(a));
								 }
							 });
			},
			close: function() {
							 this.context.close({
								 success: (a) => {
									 console.log("livePusher.close:" + JSON.stringify(a));
								 }
							 });
			},
			snapshot: function() {
							 this.context.snapshot({
								 success: (e) => {
									 console.log(JSON.stringify(e));
								 }
							 });
			},
			resume: function() {
							 this.context.resume({
								 success: (a) => {
									 console.log("livePusher.resume:" + JSON.stringify(a));
								 }
							 });
			},
			pause: function() {
							 this.context.pause({
								 success: (a) => {
									 console.log("livePusher.pause:" + JSON.stringify(a));
								 }
							 });
			},
			stop: function() {
							 this.context.stop({
								 success: (a) => {
									 console.log(JSON.stringify(a));
								 }
							 });
			},
			switchCamera: function() {
							 this.context.switchCamera({
								 success: (a) => {
									 console.log("livePusher.switchCamera:" + JSON.stringify(a));
								 }
							 });
			},
			startPreview: function() {
							 this.context.startPreview({
								 success: (a) => {
									 console.log("livePusher.startPreview:" + JSON.stringify(a));
								 }
							 });
			},
			stopPreview: function() {
							 this.context.stopPreview({
								 success: (a) => {
									 console.log("livePusher.stopPreview:" + JSON.stringify(a));
								 }
							 });
			},
			
			follow(){
				this.uPop = true
				this.pop_follw = false
			},
			cancel_follow(){
				this.uPop = false
				this.pop_follw = true
				setTimeout(()=>{
					this.pop = true
					this.pop_setInt()
				},2000)
			},
			comment_text(e){
				this.com_text = e.detail.value
				
			},
			send(){
				var content = this.com_text
				if(content!=''){
					var com_list = this.com_list
					com_list.push(content)
					this.com_list = com_list
					this.com_text = ''
					this.doms = 'po'+ com_list.length
					this.scrolTop = com_list.length*40
					// console.log('scrolTop',this.scrolTop)
					// console.log('com_list',com_list)
					
				}else{
					uni.showToast({
						title:'弹幕内容不能为空'
					})
				}
			},
				
			zan(){
				uni.vibrate({
					success:function(){
						console.log('点赞成功')
					}
				})
			},
			pop_setInt(){
				var pop_intval = setInterval(()=>{
					var pop_time = this.pop_time
					if(pop_time>=15){
						clearInterval(pop_intval)
						this.pop_time = 0
						this.pop = false,
						this.pop_follw = false
					}else{
						pop_time++
						this.pop_time = pop_time
						// console.log('pop_time',pop_time)
					}
					
				},1000)
			}
			
		}
	}
</script>

<style lang="scss" scoped>
	page{
		width: 100%;
		height: 100%;
	}
	::-webkit-scrollbar {
			width: 0;
			height: 0;
			background-color: transparent;
		} 
	.back_img{
		width: 750rpx;
		height: 100%;
		background-color: black;
	}
		
	.player_view{
		position: absolute;
		z-index: 999;
		top: 0;
		left: 0;
		.tp_user{
			width:330rpx;
			height:70rpx;
			background:rgba(0,0,0,0.2);
			// opacity:0.3;
			border-radius:32px;
			margin-left: 40rpx;
			margin-top: 70rpx;
			display: flex;
			align-items: center;
			justify-content:space-between;
			image{
				width: 70rpx;
				height: 70rpx;
				border-radius: 50%;
				background-color: #EAA34C;
			}
			.content{
				display: flex;
				flex-direction: column;
				height: 100%;
				justify-content: center;
				.text{
					font-size: 24rpx;
					color:rgba(255,255,255,1);
				}
			}
			.follow{
				width:82rpx;
				height:52rpx;
				background:rgba(234,163,76,1);
				border-radius:26px;
				text-align: center;
				line-height: 52rpx;
				font-size: 26rpx;
				color: white;
				margin-right: 20rpx;
			}
		}
		.zan_view{
			position: relative;
			top: 26rpx;
			left: 40rpx;
			width:140rpx;
			height:35rpx;
			background:rgba(0,0,0,0.2);
			border-radius:15px;
			display: flex;
			align-items: center;
			justify-content: space-around;
			image{
				width: 23rpx;
				height: 20rpx;
			}
			view{
				font-size: 20rpx;
				color: white;
			}
		}
		.home_id_view{
			position: fixed;
			top: 206rpx;
			right: 45rpx;
			width:136rpx;
			height:90rpx;
			padding-top: 5rpx;
			background:rgba(0,0,0,0.2);
			border-radius:8px;
			display: flex;
			flex-direction: column;
			align-items: center;
			justify-content: center;
			image{
				width: 106rpx;
				height: 26rpx;
			}
			view{
				color: white;
				font-size:26rpx;
				color:rgba(255,255,255,1);
			}
		}
		.pop_view{
			position: fixed;
			left: 40rpx;
			top:223rpx;
			display: flex;
			image{
				width: 226rpx;
				height: 66rpx;
				margin-right: 18rpx;
			}
		}
		.tips_view{
			position: fixed;
			left: 30rpx;
			bottom: 349rpx;
			width:470rpx;
			height:150rpx;
			background:rgba(0,0,0,0.2);
			border-radius:16px;
			font-size: 26rpx;
			color:rgba(226,211,169,1);
			padding:15rpx;
		}
		.comment_list{
			position: fixed;
			left: 30rpx;
			z-index: 999;
			bottom: 158rpx;
			width: 350rpx;
			max-height: 450rpx;
			display: flex;
			flex-direction: column;
			justify-content: end;
			overflow: hidden;
			// background-color: gray;
			yinying{
				position: relative;
				z-index: 1001;
				width: 291rpx;
				height: 40rpx;
				background:rgba(0,0,0,0.5);
			}
			// border: 1rpx solid black;
			.com_item{
				display: flex;
				min-width: 320rpx;
				max-width:348rpx;
				// min-height: 40rpx;
				background:rgba(0,0,0,0.2);
				border-radius:20px;
				align-items: center;
				margin-bottom: 15rpx;
				padding-right: 15rpx;
				.com_name{
					margin-left: 15rpx;
					font-size:26rpx;
					color:rgba(226,211,169,1);
					 white-space:nowrap;
				}
					
				.com_content{
					min-width: 100rpx;
					font-size:26rpx;
					color: white;
					margin-left: 20rpx;
				}
			}
		}
		.comment{
			position: fixed;
			bottom: 68rpx;
			left:30rpx;
			width:270rpx;
			height:72rpx;
			background:rgba(0,0,0,0.2);
			// opacity:0.3;
			border-radius:36px;
			input{
				width: 220rpx;
				height: 100%;
				padding-left: 32rpx;
				color: white;
				text-overflow:hidden;
			}
		}
		.bottom_btn{
			position: fixed;
			right: 0;
			bottom:70rpx;
			display: flex;
			.btn_view{
				width: 70rpx;
				display: flex;
				flex-direction: column;
				align-items: center;
				margin-right: 30rpx;
				image{
					width: 70rpx;
					height: 70rpx;
				}
				view{
					margin-top: 10rpx;
					font-size:18rpx;
					font-family:PingFang SC;
					// font-weight:bold;
					color:rgba(255,255,255,1);
				}
			}
		}
	}
</style>
