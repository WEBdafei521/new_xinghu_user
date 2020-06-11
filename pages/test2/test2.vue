<template>
	<view class="dis j_c al_c" style="width:100%；">
		 <!-- <image :src="imgurl" mode="aspectFill" @longpress="saveImage"></image> -->
		<canvas style="width: 507rpx; height: 664rpx;" 
		canvas-id="mycanvas"
		@longtap="saveImage"></canvas>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				// imgurl:''
			};
		},
		onLoad(){
			// this.canvasImage()
		},
		onReady(){
			this.canvasImage()
		},
		methods:{
			canvasImage(){
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
						fail: () => {
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

<style lang="scss">
	
	canvas{
		
		// border: 1rpx solid black;
		// box-shadow:0 0 9rpx 10rpx #333;
		margin-top:200rpx;
		border-radius: 10px;
	}
	image{
		width: 507rpx;
		height: 664rpx;
		display: block;
	}
	
</style>
