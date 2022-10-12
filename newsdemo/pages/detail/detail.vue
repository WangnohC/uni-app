<template>
	<view class="content-box">
		<view class="title">{{title}}</view>
		<view class="content">
			<rich-text :nodes="content"></rich-text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: "",
				content: ""
			}
		},
		onLoad(e) {
			uni.showLoading({
				title: 'Loading...',
				mask: false
			});
			uni.request({
				url: 'https://unidemo.dcloud.net.cn/api/news/36kr/' + e.post_id,
				method: 'GET',
				data: {},
				success: res => {
					this.title = res.data.title;
					this.content = res.data.content;
					uni.hideLoading();
				},
				fail: () => {},
				complete: () => {}
			});
		},
		methods: {
			
		}
	}
</script>

<style>
	.content-box {
		padding:10upx 6%; 
		width: 88%; 
		flex-wrap:wrap;
	}
	.title {
		line-height: 2em; 
		font-weight: 700; 
		font-size: 38upx;
	}
	.content {
		line-height: 2em;
	}
</style>
