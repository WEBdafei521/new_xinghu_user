<template>
	<view>
		<view class="edit_v dis cl al_c">
			<view class="itm dis al_c">
				<view class="title">直播标题</view>
				<input class="input" 
				placeholder="写个标题吸引更多粉丝" 
				placeholder-style="font-size:25rpx;color:rgba(177,177,182,1);" 
				type="text" :value="title" @input="title" />
			</view>
			<view class="itm dis al_c">
				<view class="title">内容简介</view>
				<input class="input" 
				placeholder="介绍直播内容或注意事项" 
				placeholder-style="font-size:25rpx;color:rgba(177,177,182,1);" 
				type="text" :value="title" @input="title" />
			</view>
			<view class="itm dis al_c">
				<view class="title">直播类目</view>
				<input class="input" 
				placeholder="写个标题吸引更多粉丝" 
				placeholder-style="font-size:25rpx;color:rgba(177,177,182,1);" 
				type="text" :value="title" @input="title" />
			</view>
			<view class="itm dis al_c" style="border-bottom: 1rpx solid white;">
				<view class="title">关联商品</view>
				<input class="input" 
				placeholder="写个标题吸引更多粉丝" 
				placeholder-style="font-size:25rpx;color:rgba(177,177,182,1);" 
				type="text" :value="title" @input="title" />
			</view>
		</view>
		  <view class="submit">保存</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		}
	}
</script>

<style lang="scss">
	page{
		width: 100%;
		background-color: #F8F8F8;
	}
.edit_v{
	width: 100%;
	// height: 309rpx;
	background-color: white;

	.itm{
		width:696rpx ;
		height: 70rpx;
		border-bottom: 1rpx solid #E3E3E3;
		margin-top: 20rpx;
		align-items: center;
		line-height: 80rpx;
		// background-color: gray;
		.title{
			font-size:25rpx;
			font-weight:bold;
			color:rgba(51,51,51,1);
		}
		.input{
			width: 350rpx;
			font-size:25rpx;
			margin-left: 26rpx;
		}
	}
}
	.submit{
		width:700rpx;
		height:85rpx;
		line-height: 85rpx;
		background:rgba(215,185,117,1);
		border-radius:10px;
		text-align: center;
		font-size:26rpx;
		font-family:PingFang SC;
		font-weight:bold;
		color:rgba(255,255,255,1);
		margin: 80rpx 30rpx 0 30rpx;
	}
</style>
