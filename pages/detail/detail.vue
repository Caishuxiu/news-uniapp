<template>
	<view class="detail">
		<view class="title">{{detail.title}}</view>
		<view class="info">
			<view class="author">编辑：{{detail.author}}</view>
			<view class="posttime">{{detail.posttime}}</view>
		</view>
		<view class="content">
			<rich-text :nodes="detail.content"></rich-text>
		</view>
		<view class="description">
			声明：本站内容均采集于网络，只做教学使用，谢谢您的支持。
		</view>		
	</view>
</template>

<script>
	import {parseTime} from "@/utils/tool.js"
		
	export default {
		data() {
			return {
				options: null,
				detail: {}
			}
		},
		onLoad(e){	
			// console.log(e)
			this.options = e;
			this.getDetail();
		},
		methods:{
			getDetail() {
				uni.request({
					url: "https://ku.qingnian8.com/dataApi/news/detail.php",
					data: this.options,
					success: res => {
						// console.log(res)
						res.data.content = res.data.content.replace(/<img/gi, '<img style="max-width: 100%"')
						this.detail = res.data
					}
				})
			}
		}
	}
</script>

<style lang="scss">
.detail {
	padding: 25rpx;
	.title {
		font-size: 46rpx;
		color: black;
	}
	.info {
		background-color: #f6f6f6;
		padding: 20rpx 20rpx;
		font-size: 25rpx;
		color: #666;
		display: flex;
		justify-content: space-between;
		margin: 25rpx 0;
	}
	.content {
		padding-top: 25rpx;
		padding-bottom: 50rpx;
	}
	.description {
		background: #FEF0F0;
		font-size: 26rpx;
		padding:20rpx;
		color:#F89898;
		line-height: 1.8em;
	}
}
</style>