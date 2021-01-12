<template>
	<view class="content">
		<view>二维码数据是：{{result}}</view>
		<button class="btn" type="primary" @tap="open">打开扫码</button>
	</view>

</template>

<script>
	export default {
		data() {
			return {
				result: '' //获取到的二维码内容

			}
		},

		methods: {
			open() {
				uni.navigateTo({
					url: '../text/text'
				});
			}
		},

		onShow() {
			let pages = getCurrentPages();
			let currPage = pages[pages.length - 1];
			if (currPage.data) {
				this.result = currPage.data.result
				console.log(this.result, currPage.data.result, '扫码返回')
			}

		},


	}
</script>

<style>
	.content {
		width: 100%;
		display: flex;
		flex-direction: column;
		justify-content: center;
		align-items: center;
	}

	.btn {
		width: 50%;
	}
</style>
