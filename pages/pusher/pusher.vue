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
					<view class="text" style="font-size:22rpx">00.00.00</view>
				</view>
			</view>
			
			<!-- 房间号 -->
			<view class="home_id_view">
				<image src="/static/home_name.png" mode=""></image>
				<view>ID:0001</view>
			</view>
			<view class="pusher_msg dis cl">
				<view>666点赞 666观看 666点赞</view>
				<view>网速：0kb/s</view>
				<view>已使用1.2G/剩余23G</view>
			</view>
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
				<view class="com_item" v-for="(item,index) in com_list" :key="item.index">
					<view class="com_name">
						吃货大王呀：
					</view>
					<view class="com_content">{{item}}</view>
				</view>
			</scroll-view>
			<view class="comment">
				<input type="text" 
				:value="com_text" 
				placeholder="回复粉丝..." 
				placeholder-style="font-size:26rpx;color:white" 
				confirm-type="send"
			
				@confirm="send"
				@input="comment_text" />
			</view>
			<view class="rit_btn">
				<view class="itm">
					<image src="/static/pusher/rit_icon1.png" mode=""></image>
					<view>翻转</view>
				</view>
				<view class="itm" @click="meiyan">
					<image src="/static/pusher/rit_icon2.png" mode=""></image>
					<view>美颜</view>
				</view>
				<view class="itm">
					<image src="/static/pusher/rit_icon3.png" mode=""></image>
					<view>公告</view>
				</view>
				<view class="itm">
					<image src="/static/pusher/rit_icon4.png" mode=""></image>
					<view>素材</view>
				</view>
			</view>
			<view class="bottom_btn">
				<view class="btn_view" @click="goods">
					<image src="/static/pusher/btm_icon1.png" mode=""></image>
					<view>商品</view>
				</view>
				<view class="btn_view" @click="share">
					<image src="/static/pusher/btm_icon2.png" mode=""></image>
					<view>分享</view>
				</view>
				<view class="btn_view" @click="open">
					<image src="/static/pusher/btm_icon3.png" mode=""></image>
					<view>更多</view>
				</view>
				<view class="btn_view" @click="zan">
					<image src="/static/pusher/btm_icon4.png" mode=""></image>
					<view>结束</view>
				</view>
			</view>
			<uni-popup   ref="popup" type="bottom" >		
				<view class="pop" >
					<!-- 商品列表 -->
					<view  v-if="pop_idx==13" style="height:418rpx">
						<uni-goods  @childFn="load_list" ></uni-goods>
					</view>
					
					<!-- 美颜 -->
					<view class="mei_v" v-if="pop_idx==9">
						<view class="itm dis jc_bet" style="width:750rpx;">
							<view class="ti">美颜</view>
							<view class="dis al_c" style="height: 25rpx;margin-right: 27rpx;">
								<image src="/static/pusher/reload.png" style="width: 24rpx;height:24rpx" mode="widthFix"></image>
								<view style="font-size:22rpx;color:rgba(177,177,182,1);">重置</view>
							</view>
						</view>
						<view class="itm dis">
							<view class="ti2">磨皮</view>
							<slider class="prog" :value="prog_vlue1"  backgroundColor="#B1B1B6" active-color="#E9A34B" block-size="12"  @change="slideChange(1)"/>
						</view>
						<view class="itm dis">
							<view class="ti2">美白</view>
							<slider class="prog" :value="prog_vlue2"  backgroundColor="#B1B1B6" active-color="#E9A34B" block-size="12"  @change="slideChange(2)"/>
						</view>
					</view>
					
					<!-- 一组按钮 -->
					<view class="top dis jc_bet" v-if="pop_idx==0||pop_idx==7">
						<view style="width:600rpx;text-align: center;margin-left:70rpx;">{{pop_tit}}</view>
						<view style="margin-right:30rpx" @click="close_pop">x</view>
					</view>
					<view class="item_view" v-if="pop_idx==0">
						<view class="itm dis cl al_c" 
						v-for="(item,index) in more_list" 
						:key="index" 
						@click="itm(item,index)">
							<view class="dis j_c al_c" style="width:50rpx;height:50rpx;">
								<image :src="item.img" mode="widthFix"></image>
							</view>
							
							<view>{{item.text}}</view>
						</view>
					</view>
					
					<!-- obs推流 -->
					<view class="pop_bod" v-if="pop_idx==7">
						<view class="tit dis al_c" style="height:27rpx;">
							<view>推流地址<text style="font-size:23rpx;color:rgba(233,51,64,1);">(私密，请勿泄露)</text></view>
							<image src="/static/pusher/wen.png" mode="widthFix"></image>
						</view>
						<view class="itm">
							<view class="ti">开播地址：</view>
							<view class="con dis jc_bet">
								<view class="t1">rtmp：//pd.1d5151dd4.cn//jdjkjddjkjddadad a  da ad =ada</view>
								<view class="t2">一键复制</view>
							</view>
						</view>
						<view class="itm">
							<view class="ti">直播间小程序路径：<text style="font-size:23rpx;font-weight: 400;color:rgba(177,177,182,1);">(公开，可内嵌到公众号文章)</text></view>
							<view class="con dis jc_bet">
								<view class="t1">rtmp：//pd.1d5151dd4.cn//jdjkjddjkjddadad a  da ad =ada</view>
								<view class="t2">一键复制</view>
							</view>
						</view>
					</view>
				</view>
				
			</uni-popup>
			
		</view>
		<view class="canvas_v">
			<canvas style="width: 507rpx; height: 664rpx;border-radius: 10px;"
			canvas-id="mycanvas"
			@longtap="saveImage" ></canvas>
		</view>
		
	</view>
</template>

<script>
	
	import uniPopup from '@/components/uni-popup/uni-popup.vue'
	import uniGoods from '../../components/uni-goods/uni-goods.vue'

	
	export default {
		components: {
	        uniPopup,
			uniGoods,
	    },
		

		data() {
			return {
				more_list:[{
						img:'/static/pusher/more_icon1.png',
						text:'镜像'
					},{
						img:'/static/pusher/more_icon2.png',
						text:'管理员'
					},{
						img:'/static/pusher/more_icon3.png',
						text:'允许转发'
					},{
						img:'/static/pusher/more_icon4.png',
						text:'编辑内容'
					},{
						img:'/static/pusher/more_icon5.png',
						text:'设置密码'
					},{
						img:'/static/pusher/more_icon6.png',
						text:'禁言管理'
					},{
						img:'/static/pusher/more_icon7.png',
						text:'OBS推流'
					},{
						img:'/static/pusher/more_icon8.png',
						text:'直播机器人'
					},
				],
				pop_tit:'更多',
				pop_idx:0,//弹出内容类型 1*8/更多 -- 9*12/侧边栏 -- 13/商品
				fullHeight:0,
				com_text:'',
				com_list:['多少钱?'],
				doms:'',
				scrolTop:500,
				btm_pop:false,
				prog_vlue1:40,
				prog_vlue2:40,
				scr_height:1000,
				canvasShow:false,
			};
		},
		onLoad() {
			uni.getSystemInfo({
				success: (res)=> {
					this.fullHeight ="height:" + res.windowHeight + "px";
					console.log(this.fullHeight);
				}
			})
		},
		onReady() {
			this.canvasImage()
				// 注意：需要在onReady中 或 onLoad 延时
				// this.context = uni.createLivePusherContext("livePusher", this);
		},
		methods:{
			load_list(e){
				this.scr_height = 418*(e.length)+100
				console.log('scr_height',this.scr_height)
			},
			open(){
				this.pop_idx = 0
				this.pop_tit = '更多'
			    this.$refs.popup.open()
			},
			close_pop(){
				 this.$refs.popup.close()
			},
			meiyan(){//美颜
				this.pop_idx = 9
				this.$refs.popup.open()
			},
			goods(){
				this.pop_idx = 13
				this.$refs.popup.open()
			},
			slideChange(e){
				
			},
			btm_po(){
				this.btm_pop = true
			},		
			itm(e,index){
				console.log('e',e)
				
				if(index==3){
					this.$refs.popup.close()
					uni.navigateTo({
						url:'/pages/editpusher/editpusher'
					})
				}else if(index==6){
					this.pop_idx = index+1
					console.log('pop_idx',this.pop_idx)
					this.pop_tit = e.text
				}
				
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
			share(){
				console.log('点击分享')
				this.canvasShow = true
				this.canvasImage()
			},
			canvasImage(){
				console.log('开始绘制')
					var context = uni.createCanvasContext('mycanvas')
					context.drawImage('../../static/test/share_bgimg.png',25,20,223,252.5);
					context.setFillStyle("#F8F8F8")
					context.fill()
					context.setFillStyle("#999999")
					context.setFontSize(11)
					context.drawImage('../../static/test/tach.png',55,295,28,28);
					context.fillText('微信扫码或长按识别',98.5,305)
					context.fillText('观看直播',120,320)
					context.draw(true,()=>{
						console.log('绘制完成')
						uni.canvasToTempFilePath({
							canvasId: 'mycanvas',
							success:(res)=>{
								console.log('保存成功',res)
								this.imgurl = res.tempFilePath;
								this.canvasShow = false;
								uni.setStorageSync('person-card',this.imgurl);
							},
							fail: (err) => {
								console.log('绘制失败',err)
								// uni.showToast({
								// 	title: '名片加载失败',
								// 	duration: 2000 
								// });
							}
						})
					})
				},
				saveImage(){
					uni.showActionSheet({
						itemList: ['保存图片','取消'], 
						success: (res) => {
							if(res.tapIndex == 0){
								uni.saveImageToPhotosAlbum({
									filePath: this.imgurl,//    图片文件路径，可以是临时文件路径也可以是永久文件路径，不支持网络图片路径
									success: () => {
										uni.showToast({
											title: '保存成功',
											duration: 2000
										});
									},
									fail: () => {
										uni.showToast({
											title: '保存失败',
											duration: 2000 
										});
									}
								});
							}
						},
						fail: function (res) {
							console.log(res.errMsg);
						}
					});
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
	.canvas_v{
		width: 507rpx; 
		height: 664rpx;
		border-radius: 10px;
		background-color: white;
		position: fixed;
		left: 121rpx;
		top:480rpx;
		z-index: 1002;
	}
	canvas{
		
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
			width:214rpx;
			height:57rpx;
			background:rgba(0,0,0,0.2);
			// opacity:0.3;
			border-radius:32px;
			margin-left: 40rpx;
			margin-top: 70rpx;
			display: flex;
			align-items: center;
			image{
				width: 57rpx;
				height: 57rpx;
				border-radius: 50%;
				background-color: #EAA34C;
			}
			.content{
				display: flex;
				flex-direction: column;
				height: 100%;
				justify-content: center;
				margin-left: 20rpx;
				.text{
					font-size: 20rpx;
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
		.mei_v{
			width: 100%;
			padding-top: 27rpx;
			.itm{
				justify-content: space-between;
				margin-bottom: 82rpx;
				.ti{
					font-size:25rpx;
					font-family:PingFang SC;
					font-weight:bold;
					color:rgba(51,51,51,1);
					margin-left: 27rpx;
				}
				.ti2{
					width:50rpx ;
					font-size:25rpx;
					font-family:PingFang SC;
					font-weight:400;
					color:rgba(51,51,51,1);
					margin:0 27rpx;
				}
				.prog{
					width: 605rpx;
					height: 7rpx;
				}
				
			}
		}
		.pop_bod{
			width: 100%;
			margin-top: 26rpx;
			.tit{
				margin-left: 27rpx;
				image{
					width: 26rpx;
					height: 26rpx;
					margin-left: 10rpx;
				}
				view{
					font-size:27rpx;
					font-family:PingFang SC;
					font-weight:bold;
					color:rgba(51,51,51,1);
				}
			}
			.itm{
				width: 100%;
				
				margin-top: 27rpx;
				.ti{
					margin-left: 27rpx;
					font-size:24rpx;
					font-family:PingFang SC;
					font-weight:bold;
					color:rgba(51,51,51,1);
				}
				.con{
					width:100%;
					justify-content: space-between;
					// background-color: gray;
					margin-top: 10rpx;
					.t1{
						margin-left: 27rpx;
						width: 504rpx;
						font-size:24rpx;
						font-family:PingFang SC;
						font-weight:400;
						color:rgba(102,102,102,1);
					}
					.t2{
						width:136rpx;
						height:38rpx;
						border:1px solid rgba(215,185,117,1);
						border-radius:19px;
						text-align: center;
						line-height: 38rpx;
						margin-right: 27rpx;
						font-size:24rpx;
						font-family:PingFang SC;
						font-weight:400;
						color:rgba(215,185,117,1);
					}
				}
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
			// z-index: 999;
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
			bottom: 78rpx;
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
		.pusher_msg{
			position: fixed;
			top: 168rpx;
			left: 36rpx;
			view{
				// width:264px;
				height:35rpx;
				line-height: 35rpx;
				background:rgba(0,0,0,0.3);
				border-radius:14px;
				padding: 0 20rpx ;
				font-size:18rpx;
				font-family:PingFang SC;
				font-weight:bold;
				color:rgba(255,255,255,0.8);
				margin-bottom: 27rpx;
			}
		}
		.rit_btn{
			position: fixed;
			right: 27rpx;
			top: 331rpx;
			display: flex;
			flex-direction: column;
			.itm{
				width: 70rpx;
				display: flex;
				flex-direction: column;
				align-items: center;
				margin-top: 45rpx;
				
				image{
					width: 41rpx;
					height: 41rpx;
				}
				view{
					margin-top: 15rpx;
					font-size:21rpx;
					font-family:PingFang SC;
					font-weight:bold;
					color:rgba(255,255,255,1);
					
				}
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
		.pop{
			// position: fixed;
			// bottom: 50;
			// left: 0;
			z-index: 1001;
			width: 100%;
			height:418rpx;
		
			background:rgba(248,248,248,1);
			border-radius:14px 14px 0px 0px;
				.top{
					width: 750rpx;
					justify-content: space-between;
					padding-top: 26rpx;
				}
				.item_view{
					width: 100%;
					display: flex;
					flex-wrap: wrap;
					.itm{
						width: 80rpx;
						margin: 40rpx 52rpx 0 52rpx;
						image{
							width: 42rpx;
							height: 30rpx;
						}
						view{
							white-space: nowrap;
							font-size:20rpx;
							font-family:PingFang SC;
							font-weight:bold;
							color:rgba(51,51,51,1);
							margin-top: 25rpx;
						}
					}
				}
			}
	}
</style>
