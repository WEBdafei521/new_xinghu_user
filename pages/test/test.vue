<template>
	<view >
		<view class="pc-container">
		        <image :src="imgurl" mode="aspectFill" @longpress="saveImage"></image>
		        <canvas canvas-id="mycanvas" style="width: 590rpx;height: 998rpx;" v-show="canvasShow"></canvas>
		        
		</view>
		<!-- <view class="can_v">
			<canvas canvas-id="mycanvas" style="width: 590rpx;height: 998rpx;" v-show="canvasShow"></canvas>
		</view> -->
	</view>
</template>

<script>
	
	export default {
	
		data() {
			return {
				imgurl:'',
				canvasShow:true,
 
				
			};
		},
		 onHide() {
		         uni.removeStorageSync('person-card');
		 },
		mounted() {
		//如果本地有图片了，直接取，解决一些页面切换canvas没有重画
				if(uni.getStorageSync('person-card')){
					this.canvasShow = false;
					this.imgurl = uni.getStorageSync('person-card');
				}else{
					this.canvasImage();
				}    
		},

		onReady() {
				// 注意：需要在onReady中 或 onLoad 延时
				this.context = uni.createLivePusherContext("livePusher", this);
		},
		methods:{
			canvasImage(){
			
				uni.showLoading({
					title:'加载中',
					mask:true
				})
				let myCanvas = uni.createCanvasContext('mycanvas', this); 
				//画布尺寸
				// 坐标(0,0) 表示从此处开始绘制，相当于偏移。
				//头像
				myCanvas.drawImage('../../static/logo.png',33,44,65,65);
				//参数：图片，左偏移，上偏移，宽，高
				//认证图标
				myCanvas.drawImage('../../static/logo.png',44,117,7,7);
				
				let phone = '12456798798';
				myCanvas.fillStyle = '#101010';
				
				let fontSize = 10;
				myCanvas.font = `${fontSize}px Arial`;//绘制文字
				myCanvas.fillText('认证',55,124);
				let fontSizea = 14;
				myCanvas.font = `${fontSizea}px Arial`;//绘制文字
				myCanvas.fillText('姓名：  木村林',124,58);
				myCanvas.fillText(`手机：  ${phone}`,124,76);
				myCanvas.fillText('专业：  木村林',124,94);
				myCanvas.fillText('邀请码：  木村林',124,112);
				
				myCanvas.fillText('这是我的二维码名片，请惠存!',49,185); 
				//二维码
				myCanvas.drawImage('../../static/logo.png',55,223,183,183);
				 
				myCanvas.fillText('扫码进入小程序',69,432);
				myCanvas.fillText('添加我的名片',103,458);  
				
				//开始绘画，必须调用这一步，才会把之前的一些操作实施
				myCanvas.draw(true,()=>{
					uni.canvasToTempFilePath({
						canvasId: 'mycanvas',
						success: (res) => {
							// 在H5平台下，tempFilePath 为 base64
							this.imgurl = res.tempFilePath;
							this.canvasShow = false;
							uni.hideLoading();
							uni.setStorageSync('person-card',this.imgurl);
						  },
						fail: () => {
							uni.showToast({
								title: '名片加载失败',
								duration: 2000 
							});
						}
					});
				});
				
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
image{
    width: 99%;
    min-height: 996rpx;
    border: 1px solid #BBBBBB;
        display: block;
}
.pc-container{
    width: 590rpx;
    height: 1000rpx;
    margin: 0 auto;
    padding-top: 46rpx;
    overflow: hidden;
}


</style>
