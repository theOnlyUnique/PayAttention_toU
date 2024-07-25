<template>
	<view class="uni-tabbar">
		<view class="uni-tabbar__item" v-for="(item,index) in tabbar" :key="index" @tap="changeTab(item)" >
			<!-- 上面使用的是字体图标，解决切换页面的时候图标会闪的效果，毕竟每切换一个页面都会闪一下不太好看，可以切换使用下面的图片方式 -->
			<view v-if="true" class="uni-tabbar__bd">
				<view class="uni-tabbar__icon">
					<img v-if="item.pagePath == pagePath" class="uni-w-42 uni-h-42" :src="item.selectedIconPath" />
					<img v-else class="uni-w-42 uni-h-42" :src="item.iconPath" />
				</view>
			</view>
			<view class="uni-tabbar__label">
				{{item.text}}
			</view>
		</view>
	</view>
</template>

<!-- 这里只是写着玩的 真正的路由在源码视图里面 -->
<script>
	export default {
		props: {
			pagePath: null
		},
		data() {
			return {
				page: 'contact',
				showPage: false,
				containerHeight: 400,
				tabbar: [{
						"pagePath": "../pages/home/home",
						"iconPath": "../static/img/home.png", //未选中tab图标路径
						"selectedIconPath": "../static/img/home.png", //选中tab图标路径
						"text": "首页",
					},
					{
						"pagePath": "../pages/index/index", //页面路径
						"text": "地图", //tab字体显示
						"iconPath": "../static/img/map.png", //未选中tab图标路径
						"selectedIconPath": "../static/img/map.png" //选中tab图标路径
					}, 
					{
						"pagePath": "../pages/my/my",
						"iconPath": "../static/img/user.png", //未选中tab图标路径
						"selectedIconPath": "../static/img/user.png", //选中tab图标路径
						"text": "我的",
					}
				]
			};
		},
		onLoad() {
			console.log(this.pagePath)
		},
		methods: {
			changeTab(item) {
				let currentPage = item.pagePath;
				// uni.showLoading({
				// 	title: '正在加载...'
				// })
				uni.redirectTo({
					url: currentPage,
					success: (e) => {
						uni.hideLoading();
					},
					fail: (e) => {
					}
				})
			},
		}
	}
</script>

<style lang="scss" scoped>
	.uni-tabbar {
		position: fixed;
		bottom: 0;
		z-index: 999;
		width: 100%;
		height: 10%;
		display: flex;
		justify-content: space-around;
		
		padding: 7rpx 0;
		box-sizing: border-box;
		background-color: #fff;
		box-shadow: 0px 10px 20px 0px rgba(75, 51, 100, 0.05);
 
		.uni-tabbar__item {
			display: flex;
			flex-direction: column;
			.uni-tabbar__bd { // tabBar单项
				.uni-tabbar__icon { // tabBar图标
					width: 54rpx;
					height: 83rpx;
					img {
						width: 100%;
						height: 100%;
					}
				}
			}
 
			.uni-tabbar__label { // tabBar文字
				font-size: 22rpx;
				// font-family: $PF-SC-Rfamily;
				font-weight: 400;
				color: #000000;
				text-align: center;
				&.active {
					background-image: linear-gradient(to right top, #1CFDF1, #B330FF);
					font-size: 22rpx;
					-webkit-background-clip: text;
					-moz-background-clip: text;
					background-clip: text;
					box-decoration-break: clone;
					-webkit-box-decoration-break: clone;
					-moz-box-decoration-break: clone;
					color: transparent;
					position: relative;
				}
			}
		}
 
		// .uni-tabbar__icon {
		// 	height: 42upx;
		// 	line-height: 42upx;
		// 	text-align: center;
		// }
 
		.icon {
			display: inline-block;
		}
 
		// .uni-tabbar__label {
		// 	line-height: 24upx;
		// 	font-size: 24upx;
		// 	color: #999;
 
		// 	&.active {
		// 		color: #1ca6ec;
		// 	}
		// }
	}
</style>