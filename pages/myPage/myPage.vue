<template>
	<view>
		<image src="/static/myPage/topImg.png"style="width:100%;height:250rpx;" ></image>
		<view class="uMsg">
			<view class="avatar dis al_c">
				<view class="dis cl al_c j_c" style="width:140rpx;height:200rpx">
					<view class="zwyPortrait" style="--color:#E93340;">
						<image  src="/static/zan.png" mode=""></image>
					</view>
					
					<!-- <view style="width: 50rpx;height: 50rpx;display: flex;align-items: center;justify-content: center;">
						<view class="zwyLive" style="--color:#D7B975;"> </view>
					</view> -->
				</view>
				<view class="edit">编辑资料</view>
			</view>
			<view class="name">红狐集团</view>
			<view class="tag_v dis al_c">
				<view>ID:0005</view>
				<image style="margin-left: 50rpx;" src="/static/myPage/icon1.png" mode="widthFix"></image>
				<image src="/static/myPage/icon2.png" mode="widthFix"></image>
				<image src="/static/myPage/icon3.png" mode="widthFix"></image>
			</view>
			<view class="shop dis al_c">
				<image src="" mode=""></image>
				<view>我的商城</view>
			</view>
			<view class="present">请填写个人简介，点击添加…</view>
			<view class="dis" style="margin-left: 50rpx;margin-top:20rpx;margin-bottom:30rpx;">
				<view style="font-size:23rpx;font-family:PingFang SC;font-weight:bold;color:rgba(51,51,51,1);">666关注</view>
				<view style="font-size:23rpx;font-family:PingFang SC;font-weight:bold;color:rgba(51,51,51,1);margin-left: 30rpx;;">666粉丝</view>
			</view>
			<view style="width:750rpx;height:15rpx;background-color: whitesmoke;"></view>
			<view class="top_view">
				<view class="item" @click="switchTap(0)">
					<view :class="['text',curindex==0?'col':'']">我的推荐</view>
					<view :class="['bord_view',curindex==0?'act':'']"> </view>
				</view>
				<view class="item" style="margin-left: 149rpx;" @click="switchTap(1)">
					<view :class="['text',curindex==1?'col':'']" >直播回放</view>
					<view :class="['bord_view',curindex==1?'act':'']"> </view>
				</view>
			</view>
			<swiper  
			:style="{height:swiperheight+'px'}"
			:indicator-dots="false" 
			:autoplay="false" 
			:interval="3000" 
			:duration="1000"
			:current="tabIndex" @change="tabChange">
				<swiper-item>
					<view class="swiper-item">
						<!-- 我的推荐 -->
						<view class="recom_list">
							<view class="recom_item">
								<view class="img_v dis cl">
									<image src="" mode=""></image>
									<view class="imgTip dis al_c">
										<view class="tag">预告</view>
										<view class="text">今天晚上18:00准时开始直播</view>
									</view>
								</view>
								<view class="tit_v dis al_c">
									<image src="" mode=""></image>
									<view class="name_v dis cl j_c">
										<view class="nm">红狐集团</view>
										<view class="gz">已关注</view>
									</view>
								</view>
							</view>
						
						</view>
					</view>
				</swiper-item>
				<swiper-item>
					<view class="swiper-item">
						<!-- 直播回放 -->
						<view class="top_tip dis al_c">
							<image src="" mode=""></image>
							<view class="content dis cl aro">
								<view class="text dis al_c" style="margin-top:10rpx">
									<view style="font-size:24rpx;">红狐集团</view>
									<view class="tag" style="border-radius: 5px;">预告</view>
								</view>
								<view style="font-size:24rpx;color:rgba(51,51,51,1);margin-bottom: 10rpx;">今天九点开始直播，有新品上新哦！</view>
							</view>
						</view>
						<view class="back_list dis cl">
							<view class="back_item dis jc_bet">
								<view class="lef dis">
									<view class="vdo_v"></view>
									<view class="content dis cl jc_bet">
										<view>内容标题</view>
										<view>858次观看 04/15</view>
									</view>
								</view>
								<view class="rit dis cl jc_end">
									<image src="/static/myPage/more.png" mode=""></image>
								</view>
							</view>
						</view>
					</view>
				</swiper-item>
			</swiper>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				curindex:0,
				tabIndex:0,
				swiperheight:500,
			};
		},
		onLoad() {
			
		},
		methods:{
			switchTap(e){
				 // console.log('e',e)
				 this.curindex = e
				 this.tabIndex = e
			},
			tabChange(e){
				 // console.log('e',e)
				 this.curindex = e.detail.current
				 this.tabIndex = e.detail.current
			}
		}
	}
</script>

<style lang="scss" scoped>
	@import '../../common/zwyCss.css';
.uMsg{
	
}
.avatar{
	height: 140rpx;
	margin-top: -20rpx;
	margin-left: 40rpx;
	image{
		width: 140rpx;
		height: 140rpx;
		border-radius: 50%;
		background-color: pink;
	}
	.edit{
		width:181rpx;
		height:45rpx;
		background:rgba(177,177,181,1);
		border-radius:25px;
		font-size:23rpx;
		text-align: center;
		line-height: 45rpx;
		font-family:PingFang SC;
		font-weight:bold;
		color:rgba(255,255,255,1);
		margin-left: 45rpx;
		margin-bottom: 10rpx;
	}
}
.name{
	font-size:30rpx;
	font-family:PingFang SC;
	font-weight:bold;
	color:rgba(51,51,51,1);
	margin-left: 50rpx;
	margin-top: 18rpx;
}
.tag_v{
	margin-left: 50rpx;
	height: 50rpx;
	view{
		font-size:23rpx;
		font-family:PingFang SC;
		font-weight:bold;
		color:rgba(51,51,51,1);
	}
	image{
		width: 27rpx;
		height: 27rpx;
		margin-left: 10rpx;
	}
}
.shop{
	width: 750rpx;
	height: 60rpx;
	border-top: 1rpx solid whitesmoke;
	border-bottom: 1rpx solid whitesmoke;
	image{
		width: 24rpx;
		height: 24rpx;
		background-color: #D7B975;
		margin-left: 50rpx;
	}
	view{
		font-size:23rpx;
		font-family:PingFang SC;
		font-weight:bold;
		color:rgba(215,185,117,1);
		margin-left: 20rpx;
	}
}
.present{
	font-size:23rpx;
	font-family:PingFang SC;
	font-weight:bold;
	color:rgba(51,51,51,1);
	margin-left: 50rpx;
	margin-top: 20rpx;
}
.top_view{
	width: 750rpx;
	height: 70rpx;
	display: flex;
	justify-content: center;
	align-items: center;
	background-color: white;
	border-bottom: 1rpx solid whitesmoke;
	.item{
		width:120rpx;
		height: 70rpx;
		line-height: 70rpx;
		display: flex;
		flex-direction: column;
		align-items: center;
		.text{
			color: black;
			
			font-size: 30rpx;
		}
		.col{
			color: #D7B975;
		}
		.bord_view{
			width: 120rpx;
			height: 4rpx;
			border-bottom: 4rpx solid #FFFFFF;
		}
			
		.act{
			border-bottom: 4rpx solid #D7B975;
		}
	}
}
.recom_list{
	display: flex;
	flex-wrap: wrap;
	.recom_item{
		width: 335rpx;
		height: 443rpx;
		background:rgba(247,247,247,1);
		border-radius:14px;
		margin: 18rpx 0 0 27rpx;
		.img_v{
			width: 100%;
			height: 335rpx;
			image{
				width: 100%;
				height: 335rpx;
			}
			.imgTip{
				width: 100%;
				height: 60rpx;
				margin-top: -60rpx;
				background:rgba(0,0,0,0.2);
				.tag{
					width:57rpx;
					height:24rpx;
					background:rgba(122,169,248,1);
					border-radius:12px;
					font-size:16rpx;
					font-family:PingFang SC;
					font-weight:bold;
					color:rgba(255,255,255,1);
					margin-left: 18rpx;
					text-align: center;
					line-height: 24rpx;
				}
				.text{
					font-size:18rpx;
					font-family:PingFang SC;
					font-weight:bold;
					color:rgba(255,255,255,1);
					margin-left: 10rpx;
				}
			}
		
		}
		.tit_v{
			width: 100%;
			image{
				width: 54rpx;
				height: 54rpx;
				border-radius: 50%;
				margin:0 27rpx;
				background-color: gray;
			}
			.name_v{
				width: 200rpx;
				height: 109rpx;
				.nm{
					font-size:24rpx;
					font-family:PingFang SC;
					font-weight:bold;
					color:rgba(51,51,51,1);
				}
				.gz{
					width: 63rpx;
					height: 24rpx;
					background:rgba(234,163,76,1);
					border-radius:12px;
					font-size:16rpx;
					font-family:PingFang SC;
					font-weight:bold;
					color:rgba(255,255,255,1);
					text-align: center;
					line-height: 24rpx;
					margin-top: 10rpx;
				}
				}
			}
	}
}
.top_tip{
	width:695rpx;
	height:100rpx;
	background:rgba(247,247,247,1);
	border-radius:14px;
	margin: 18rpx 0rpx 0rpx 27rpx;
	image{
		width: 54rpx;
		height: 54rpx;
		border-radius: 50%;
		background-color: pink;
		margin-left: 19rpx;
	}
	.content{
		height: 109rpx;
		margin-left: 17rpx;
		justify-content: space-around;
	}
}
.back_list{
	width: 750rpx;
	margin-top: 27rpx;
	.back_item{
		width: 100%;
		height: 135rpx;
		justify-content: space-between;
		.lef{
			.vdo_v{
				width: 253rpx;
				height: 135rpx;
				background-color: whitesmoke;
				border-radius:14px;
				margin-left: 24rpx;
			}
			.content{
				height: 135rpx;
				justify-content: space-between;
				margin-left: 17rpx;
				view:first-child{
					font-size:25rpx;
					font-family:PingFang SC;
					font-weight:400;
					color:rgba(51,51,51,1);
				}
				view:nth-child(2){
					font-size:21rpx;
					font-family:PingFang SC;
					font-weight:400;
					color:rgba(177,177,181,1);
				}
			}
		}
		.rit{
			width: 10rpx;
			height: 135rpx;
			justify-content: flex-end;
			margin-right: 45rpx;
			image{
				width: 10rpx;
				height: 20rpx;
			}
		}
	}
}
.tag{
		width:57rpx;
		height:24rpx;
		background:rgba(122,169,248,1);
		border-radius:12px;
		font-size:16rpx;
		font-family:PingFang SC;
		font-weight:bold;
		color:rgba(255,255,255,1);
		margin-left: 18rpx;
		text-align: center;
		line-height: 24rpx;
	}
</style>
