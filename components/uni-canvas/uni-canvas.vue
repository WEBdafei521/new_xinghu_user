<template>
	<view>
		<!-- <view>分享海报</view> -->
		<!-- 绘制分享海报 -->
		<canvas style="width: 507rpx; height: 664rpx;"
		canvas-id="mycanvas"
		@longtap="saveImage">
		</canvas>	
	</view>
</template>

<script>
	export default {
		data() {
			return {
				 imgurl:''
			};
		},
		created(){
			console.log('已加载')
			this.canvasImage()
		},
		onReady(){
			console.log('页面已加载')
			// this.canvasImage()
		},
		methods:{
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

</style>
