<template>
	<view>
	<view class="sumNum">共11件商品</view>
	<scroll-view scroll-y="true" height="200" >
		<view class="goods_list dis cl al_c">
			<view class="goods_item dis" v-for="(item,id) in goos_list" :key="item.id">
				<view class="content dis al_c">
					<image :src="item.imgUrl" mode=""></image>
					<view class="msg dis cl jc_bet" style="margin-left: 20rpx;height:156rpx">
						<view class="dis al_c" style="height:60rpx">
							<view class="tag">{{item.tag}}</view>
							<view class="name">{{item.name}}</view>
						</view>
						<view class="btm_msg dis">
							<view class="t1">￥9.9</view>
							<view class="t2">已售:10</view>
							<view class="t2">库存:110</view>
							<view class="t3">讲解此商品</view>
						</view>
					</view>
				</view>
			</view>
		</view>
	</scroll-view>
	
	</view>
</template>

<script>
	export default {
		data() {
			return {
				goos_list:[
					{
						id:'1',
						name:'日系印花连帽工装棉服男ins潮流',
						tag:'官方',//标签
						imgUrl:'/static/chu.png',
						price:'9.9',
						stock:'',//库存
						sales:'',//销量
					},
					{
						id:'2',
						name:'日系印花连帽工装棉服男ins潮流',
						tag:'官方',//标签
						imgUrl:'/static/chu.png',
						price:'9.9',
						stock:'',//库存
						sales:'',//销量
					},
					{
						id:'2',
						name:'日系印花连帽工装棉服男ins潮流',
						tag:'官方',//标签
						imgUrl:'/static/chu.png',
						price:'9.9',
						stock:'',//库存
						sales:'',//销量
					},
					{
						id:'2',
						name:'日系印花连帽工装棉服男ins潮流',
						tag:'官方',//标签
						imgUrl:'/static/chu.png',
						price:'9.9',
						stock:'',//库存
						sales:'',//销量
					},
				]
			};
		},
		
		  created: function () {
		    console.log('调用了created钩子函数')
			this.$emit('childFn', this.goos_list);
		  },

	
	}
</script>

<style lang="scss">
	.sumNum{
		font-size:27rpx;
		font-family:PingFang SC;
		font-weight:bold;
		color:rgba(51,51,51,1);
		margin: 27rpx;
		padding-top: 20rpx;
	}
	.goods_list{
		width: 100%;
		height: 318rpx;
		
		background:whitesmoke;
		.goods_item{
			width:695rpx;
			height:156rpx;
			background:rgba(255,255,255,1);
			border-radius:14px;
			margin-bottom: 20rpx;
			// border: 1rpx solid black;
			image{
				width: 164rpx;
				height: 156rpx;
				border-radius:14px;
				background-color: gray;
			}
			.content{
				height: 156rpx;
				.msg{
					justify-content: space-between;
					.name{
						font-size:24rpx;
						font-family:PingFang SC;
						font-weight:bold;
						color:rgba(51,51,51,1);
						margin-left: 15rpx;
					}
					.tag{
						width:57rpx;
						height:24rpx;
						background:linear-gradient(90deg,rgba(138,190,255,1) 0%,rgba(27,102,255,1) 100%);
						border-radius:7px;
						font-size:16rpx;
						font-family:PingFang SC;
						font-weight:bold;
						color:rgba(255,255,255,1);
						// margin-left: 18rpx;
						text-align: center;
						line-height: 24rpx;
					}
					.btm_msg{
						height: 45rpx;
						align-items: flex-end;
						padding-bottom: 10rpx;
						.t1{
							font-size:27rpx;
							font-family:PingFang SC;
							font-weight:bold;
							color:rgba(215,185,117,1);
							
						}
						.t2{
							font-size:22rpx;
							font-family:PingFang SC;
							// font-weight:bold;
							color:rgba(153,153,153,1);
							margin-left: 26rpx;

						}
						.t3{
							width:163rpx;
							height:45rpx;
							background:rgba(215,185,117,1);
							border-radius:23px;
							font-size:24rpx;
							font-family:PingFang SC;
							font-weight:bold;
							color:rgba(255,255,255,1);
							text-align: center;
							line-height: 45rpx;
							margin-left: 26rpx;
						}
					}
				}
			}
		}
	}

</style>
