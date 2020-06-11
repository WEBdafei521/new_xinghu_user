<template>
	<view>
		<image class="bg_img" src="/static/openservice/bg_img.png" mode="widthFix"></image>
		<view class="body_top">
			<!-- 会员信息 -->
			<view class="uMessage dis j_c">
				<view class="dis cl al_c" style="width: 150rpx;">
					<view class="top_num">125天</view>
					<view class="top_text">剩余会员天数</view>
				</view>
				<view class="dis cl al_c" style="margin:0 90rpx;">
					<image src="" style="width:77rpx;height:77rpx;background-color:white;border-radius: 50%;" mode=""></image>
					<view style="font-size:27rpx;color:rgba(185,185,185,1);margin-top:23rpx;">红狐集团</view>
				</view>
				<view class="dis cl al_c" style="width: 150rpx;">
					<view class="top_num">2020/08/11</view>
					<view class="top_text">会员有效期至</view>
				</view>
			</view>
			<!-- 特权卡片 -->
			<swiper class="swiper" 
				:indicator-dots="false" 
				:autoplay="false" 
				:interval="3000" 
				:duration="700"
				previous-margin="30"
				next-margin="30"
				current="1">
					<swiper-item>
						<view class="swiper-item"></view>
					</swiper-item>
					<swiper-item>
						<view class="swiper-item" >
							<image  src="/static/openservice/bg_card.png" style="width:100%;height:100%" 
							mode="widthFix"></image>
							<view class="sp-item">
								<!-- <image class="vip_icon" src="/static/openservice/vip_icon.png" style="width:176rpx;height:105rpx;" mode="widthFix"></image> -->
								<view class="tag-left"></view>
								<view class="dis jc_bet" style="width:100%;margin-top: 45rpx;">
									<view class="list dis cl">
										<view class="li dis">
											<view style="width:120rpx;">技术服务费</view>
											<view style="margin-left: 70rpx;">￥19800/年</view>
										</view>
										<view class="li dis">
											<view style="width:120rpx;">服务类型</view>
											<view style="margin-left: 70rpx;">志同道合合伙人</view>
										</view>
										<view class="li dis" style="margin: 0;">
											<view style="width:120rpx;">我的邀请人</view>
											<view style="margin-left: 70rpx;">请确认绑定邀请人</view>
										</view>
										<view style="font-size:19rpx;color:gray;margin-left: 190rpx;margin-top:10rpx">(点击修改)</view>
									</view>
									<view class="open">立即开通</view>
									
								</view>	
							</view>
						</view>
					</swiper-item>
					<swiper-item>
						<view class="swiper-item"></view>
					</swiper-item>
			</swiper>
			<view class="card_view">
				<view class="title">直播特权</view>
				<view class="itme_view dis aro">
					<view class="car_item dis cl al_c">
						<image src="/static/openservice/icon1.png" mode=""></image>
						<view>随时随地直播</view>
					</view>
					<view class="car_item dis cl al_c">
						<image src="/static/openservice/icon1.png" mode=""></image>
						<view>主播视频转播</view>
					</view>
					<view class="car_item dis cl al_c">
						<image src="/static/openservice/icon1.png" mode=""></image>
						<view>可绑个人子账号</view>
					</view>
				</view>
				<view class="tip">还有更多特权等你来尽享</view>
			</view>
			<view class="card_view">
				<view class="title">商城特权</view>
				<view class="itme_view dis aro">
					<view class="car_item dis cl al_c">
						<image src="/static/openservice/icon1.png" mode=""></image>
						<view>拥有个人商城</view>
					</view>
					<view class="car_item dis cl al_c">
						<image src="/static/openservice/icon1.png" mode=""></image>
						<view>转载主播商品</view>
					</view>
					<view class="car_item dis cl al_c">
						<image src="/static/openservice/icon1.png" mode=""></image>
						<view>选购官方商池</view>
					</view>
				</view>
				<view class="tip">还有更多特权等你来尽享</view>
			</view>
			<view class="bottom_content dis cl al_c">
				<view class="title dis j_c al_c">
					<view class="line_l"> </view>
					<view class="text">技术服务内容</view>
					<view class="line_r"> </view>
				</view>
				<view class="btm_tips">用户根据各自需求缴纳对应的技术服务费，即可获取更多更方便的 推广、更有效的做营销展示、个更全面拓展社交渠道价值，更直接 的实现</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				imageBase64: ''
				
			};
		}
	}
</script>

<style lang="scss">
page{
	width: 100%;
	background-color: whitesmoke;
	
}
.bg_img{
	width: 100%;
	height: 750rpx;
}
.uMessage{
	padding-top: 40rpx;
}
.top_num{
	font-size:27rpx;
	font-family:PingFang SC;
	font-weight:bold;
	color:rgba(229,201,155,1);
	background:linear-gradient(0deg,rgba(248,225,180,1) 0%, rgba(193,153,98,1) 100%);
	-webkit-background-clip:text;
	-webkit-text-fill-color:transparent;
}
.top_text{
	font-size:21rpx;
	font-family:PingFang SC;
	font-weight:400;
	color:rgba(184,184,184,1);
}
.body_top{
	width: 750rpx;
	height:750rpx;
	// background-color: #232323;
	position: absolute;
	z-index: 999;
	top:150rpx;
	left: 0;
}
.swiper{
	width: 750rpx;
	height: 300rpx;
	margin-top: 110rpx;
}
.swiper-item{
	width: 610rpx;
	height: 290rpx;
	// background:linear-gradient(115deg,rgba(230,215,182,1) 0%,rgba(241,234,217,1) 25%,rgba(186,168,126,1) 100%);
	
	border-radius:14px;
	margin-left: 10rpx;
	padding-top: 14rpx;
	.vip_icon{
		
		
		// margin-top: -395rpx;
	}
	.sp-item{
		position: relative;
		z-index: 999;
		top: -290rpx;
	}
	.tag-left{
		width:153rpx;
		height:50rpx;
		// background:linear-gradient(90deg,rgba(67,67,67,1) 0%,rgba(29,30,32,1) 100%);
		// border-radius:0px 22px 22px 0px;
		// color: #E7D9B9;
		// font-size:23rpx;
		// text-align: center;
		// line-height: 50rpx;
	}
	.list{
		margin: 27rpx 0 0 27rpx;
		.li{
			margin-bottom: 12rpx;
			view{
				font-size:23rpx;
				font-family:PingFang SC;
				font-weight:bold;
				color:rgba(51,51,51,1);
			}
		}
	}
	.open{
		width:165rpx;
		height:50rpx;
		background:rgba(133,109,49,1);
		border-radius:25px;
		font-size:27rpx;
		text-align: center;
		line-height: 50rpx;
		font-family:PingFang SC;
		font-weight:400;
		color:rgba(255,255,255,1);
		margin-top: 95rpx;
		margin-left: 40rpx;
	}
}
.card_view{
	width:695rpx;
	height:289rpx;
	background:rgba(255,255,255,1);
	border-radius:14px;
	margin: 27rpx;
	padding-top: 27rpx;
	.title{
		font-size:27rpx;
		font-family:PingFang SC;
		font-weight:bold;
		color:rgba(51,51,51,1);
		margin-left: 27rpx;
	}
	.itme_view{
		width: 100%;
		margin-top: 39rpx;
		.car_item{
			width: 160rpx;
			image{
				width: 81rpx;
				height: 81rpx;
				border-radius: 50%;
				// background:linear-gradient(0deg,rgba(232,207,160,1) 0%,rgba(221,190,140,1) 100%);
				
			}
			view{
				font-size:23rpx;
				font-family:PingFang SC;
				font-weight:bold;
				color:rgba(51,51,51,1);
				margin-top: 18rpx;
			}
		}
		image{
			width: 81rpx;
			height: 81rpx;
		}
	}
		
	.tip{
		width: 100%;
		text-align: center;
		font-size:21rpx;
		font-family:PingFang SC;
		font-weight:400;
		color:rgba(179,140,89,1);
		margin-top: 27rpx;
	}
}
.bottom_content{
	width: 100%;
	margin-top: 44rpx;
	.line_l{
		width: 185rpx;
		height: 1rpx;
		background:linear-gradient(270deg,rgba(51,51,51,1) 0%,rgba(51,51,51,0) 100%);
	}
	.line_r{
		width: 185rpx;
		height: 1rpx;
		background:linear-gradient(90deg,rgba(51,51,51,1) 0%,rgba(51,51,51,0) 100%);
	}
		
	.title{
		height: 50rpx;
	}
	.text{
		font-size:27rpx;
		font-family:PingFang SC;
		font-weight:bold;
		color:rgba(51,51,51,1);
		margin: 0 10rpx;
	}
		
	.btm_tips{
		font-size:21rpx;
		font-family:PingFang SC;
		font-weight:400;
		color:rgba(153,153,153,1);
		margin: 36rpx;
	}
}
</style>
