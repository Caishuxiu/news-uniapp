<template>
	<view class="newsbox">
		<view class="text">
			<view class="title">{{item.title}}</view>
			<view class="info" v-if="!item.watchtime">
				<text>{{item.author}}</text>
				<text>总浏览量 {{item.hits}}</text>
			</view>
			<view class="info" v-else>
				<text>浏览时间：{{item.watchtime}}</text>
			</view>
		</view>
		<view class="pic">
			<image :src="item.picurl" mode="aspectFill"></image>
		</view>
	</view>
</template>

<script>
	export default {
		name:"newsbox",
		props: {
			item: {
				type: Object,
				default() {
					return {
						title: "组件内默认的标题（懒得写了...）",
						author: "张三",
						hits: 123,
						picurl: "../../static/images/nopic.jpg"
					}
				}
			}
		},
		data() {
			return {
				
			};
		}
	}
</script>

<style lang="scss">
.newsbox {
	display: flex;
	.text {
		// border: 1px solid red;
		flex: 1;
		display: flex;
		flex-direction: column;
		justify-content: space-between;
		padding-right: 30rpx;
		.title {
			font-size: 38rpx;
			overflow: hidden;
			text-overflow: ellipsis;
			display: -webkit-box;
			-webkit-line-clamp: 2;
			-webkit-box-orient: vertical;
		}
		.info {
			font-size: 25rpx;
			color: #9499a0;
			text {
				padding-right: 30rpx;
			}
		}
	}
	.pic {
		width: 200rpx;
		height: 160rpx;
		// border: 1px solid red;
		image {
			width: 100%;
			height: 100%;
			border-radius: 18rpx;
		}
	}
}
</style>