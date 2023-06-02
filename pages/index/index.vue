<template>
	<view class="uni-list">
		<view class="uni-list-cell" hover-class="uni-list-cell-hover" v-for="(item,index) in news" :key="index" @click="openDetail(item.post_id)">
			<view class="uni-media-list">
				<image class="uni-media-list-logo" :src="item.author_avatar"></image>
				<view class="uni-media-list-body">
					<view class="uni-media-list-text-top">{{item.title}}</view>
					<view class="uni-media-list-text-bottom uni-ellipsis">{{item.content}}</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				news: []
			}
		},
		onLoad() {
			uni.showLoading({
				title: 'Loading...',
				mask: false
			});
			uni.request({
				url: 'https://unidemo.dcloud.net.cn/api/news',
				method: 'GET',
				data: {},
				success: res => {
					this.news = res.data;
					uni.hideLoading();
				},
				fail: () => {},
				complete: () => {}
			});
		},
		methods: {
			openDetail(post_id) {
				uni.navigateTo({
					url: '../detail/detail?post_id=' + post_id,
					success: res => {},
					fail: () => {},
					complete: () => {}
				});
				
			}
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}
	.uni-media-list-body {
		height: auto;
	}
	.uni-media-list-text-top {
		line-height:1.6em;
	}
</style>
