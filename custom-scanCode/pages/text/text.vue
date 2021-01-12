<template>
	<view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				name: '', //要在扫码界面自定义的内容
				flash: false, //是否打开摄像头
				type: '',
				barcode:null
			};
		},
		onLoad(d) {
			var currentWebview = plus.webview.currentWebview()
			var barcode = plus.barcode.create('barcode', [plus.barcode.QR], {  
			    top:'45px',  
			    left:'0px',  
			    width: '100%',  
			    height: '90%',  
			    position: 'static'  
			});  
			this.barcode = barcode
			 // 扫码识别成功
			  barcode.onmarked = (type, result) => {
				  console.log(result,'扫码结果')
				  var text = '未知: ';
				  switch (type) {
				  	case plus.barcode.QR:
				  		text = 'QR: ';
				  		break;
				  	case plus.barcode.EAN13:
				  		text = 'EAN13: ';
				  		break;
				  	case plus.barcode.EAN8:
				  		text = 'EAN8: ';
				  		break;
				  }
				  var pages = getCurrentPages(); //当前页面
				  var prevPage = pages[pages.length - 2]; //上一页面
				  prevPage.data = {
				  	//直接给上一个页面赋值
				  	result: result
				  }
				  uni.navigateBack({
				  	delta: 1
				  });
				  barcode.close();
			  }
			  barcode.onerror = (error) => {
				 uni.showToast({
				 	title:'扫码失败',
					icon:'none'
				 })
				 uni.navigateBack({
				 	delta: 1
				 });
				 barcode.close();
			  }
			currentWebview.append(barcode);
		},
		onBackPress() {
			var currentWebview = plus.webview.currentWebview()
			currentWebview.append('');
			this.barcode.close();
		},
		methods: {

		},
	}
</script>

<style scoped>
	.topHeader {
		width: 100%;
		height: 100rpx;
		background-color: #F8F8F8;
	}
</style>
