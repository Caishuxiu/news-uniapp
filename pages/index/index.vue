<template>
	<view class="home">	
		<scroll-view class="navScroll" scroll-x>
			<view class="item" v-for="(item, index) in navArr"
			@click="clickNav(item.id)"
			:key="item.id">
				<image class="navPic" :src="imageUrl[index]" mode="aspectFill"></image>
				<p class="category">{{item.classname}}</p>
			</view>			
		</scroll-view>
		
		<view class="color-wrap">
			<swiper class="recommended" indicator-dots autoplay interval="2000" circular>
				<swiper-item v-for="item in swiperArr">
					<image class="swiperPic" :src="item.picurl"></image>
					<view class="text">
						<view class="title">{{item.title}}</view>
						<view class="info">
							<text>{{item.author}}</text> 
							<text>总浏览量 {{item.hits}}</text>
						</view>	
					</view>
				</swiper-item>
			</swiper>
		</view>
		
		<view class="content">
			<div class="row" v-for="item in newsArr" :key="item.id">
				<newsbox :item="item" @click.native="goDetail(item)"></newsbox>
			</div>
		</view>	
				
		<view class="nodata" v-if="!newsArr.length">
			<image src="../../static/images/nodata.png" mode="widthFix"></image>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				navIndex: 0,
				imageUrl: ['../../static/images/internal.png', '../../static/images/external.png', '../../static/images/sport.png', '../../static/images/science.png', '../../static/images/fashion.png', '../../static/images/leisure.png'],
				navArr: [],
				newsArr: [],
				currentPage: 1,
				currentId: 50,
				swiperArr : []
			}
		},
		onLoad() {
			this.getNavData();
			this.getNewsData();
			this.getSwiperData();
		},
		onReachBottom() {
			// console.log("到底部了")
			this.currentPage++;
			// console.log(this.currentPage)
			this.getNewsData(this.currentId);
		},
		methods: {
			// 点击导航切换
			clickNav(id){
				// console.log(id)
				this.currentPage = 1;
				this.newsArr = [];
				this.currentId = id;
				// console.log(this.currentId)
				this.getNewsData(id);
			},
			
			// 跳转到详情页
			goDetail(item) {
				// console.log(item)
				uni.navigateTo({
					url: `/pages/detail/detail?cid=${item.classid}&id=${item.id}`
				})
			},
			
			// 获取导航列表数据
			getNavData() {
				uni.request({
					url: "https://ku.qingnian8.com/dataApi/news/navlist.php",
					success: res => {
						// console.log(res)
						this.navArr = res.data
					}
				})
			},
			
			// 获取资讯列表数据
			getNewsData(id=50) {
				uni.request({
					url: "https://ku.qingnian8.com/dataApi/news/newslist.php",
					data: {
						cid: id,
						num: 8,
						page: this.currentPage
					},
					success: res => {
						// console.log(res)
						this.newsArr = [...this.newsArr, ...res.data]
					}
				})
			},
			
			// 获取轮播列表数据
			getSwiperData() {
				uni.request({
					url: "https://ku.qingnian8.com/dataApi/news/newslist.php",
					data: {
						cid: 53,
						num: 3
					},
					success: res => {
						// console.log(res)
						this.swiperArr = res.data
					}
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
.navScroll {
	height: 230rpx;
	background-color: white;
	white-space: nowrap;
	/deep/ ::-webkit-scrollbar {
		width: 4px !important;
		height: 1px !important;
		overflow: auto !important;
		background: transparent !important;
		-webkit-appea3ance: auto !important;
		display: block;
	}
	.item {
		display: inline-block;
		padding: 25rpx 20rpx;
		position: relative;
		.navPic {
			width: 180rpx;
			height: 180rpx;
			border: 7rpx solid #3a87c0;
			border-radius: 30rpx;
			}
		.category {
			color: white;
			font-size: 30rpx;
			position: absolute;
			left: 85rpx;
			bottom: 50rpx;
		}
	}	
}
.content {
	padding: 0 25rpx;
	// border: 1px solid pink;
	.row {
		border-bottom: 1rpx dotted #3a87c0;
		padding: 25rpx 0;
	}
}
.color-wrap {
	background-color: #f1f3f4;
	padding: 25rpx;
}
.recommended {
	height: 390rpx;
	// border: 2px solid black;
	border-radius: 30rpx;
	overflow: hidden;
	.swiperPic {
		width: 100%;
	}
	.text {
		// border: 2px solid pink;
		color: white;
		// padding-bottom: 10rpx;
		position: absolute;
		left: 25rpx;
		right: 25rpx;
		bottom: 0px;
		.title {
			font-size: 38rpx;
			margin-bottom: 5rpx;
		}
		.info {
			font-size: 20rpx;
			text {
				padding-right: 30rpx;
			}
		}
	}
}
.nodata {
	display: flex;
	justify-content: center;
	image {
		width: 360rpx;
	}
}
</style>