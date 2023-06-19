<template>
	<view class="bookmarks">	
		<view class="row" v-for="item in 10">
			<newsbox @click.native="goDetail"></newsbox>
		</view>	
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},  
		methods: {
			// 跳转到详情页
			goDetail() {
				uni.navigateTo({
					url: "/pages/detail/detail"
				})
			}
			
			
			
		}
	}

</script>

<style lang="scss">
.bookmarks {
	padding: 0 25rpx;
	// border: 1px solid pink;
	.row {
		border-bottom: 1rpx dotted #3a87c0;
		padding: 25rpx 0;
	}
}
</style>