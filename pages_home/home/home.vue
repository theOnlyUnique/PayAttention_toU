<template>
	<view>
		<view class="uni-margin-wrap">
			<swiper class="swiper" circular :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval"
				:duration="duration">
				<swiper-item>
					<view class="swiper-item uni-bg-red">
						<image src="../../static/img/logo1.png" class="swiper-image"></image>
					</view>
				</swiper-item>
				<swiper-item>
					<view class="swiper-item uni-bg-green">
						<image src="../../static/img/logo2.png" class="swiper-image"></image>
					</view>
				</swiper-item>
				<swiper-item>
					<view class="swiper-item uni-bg-blue">
						<image src="../../static/img/logo3.png" class="swiper-image"></image>
					</view>
				</swiper-item>
			</swiper>
		</view>
		
		<uni-section title="卡片封面图+操作栏" type="line">
					<uni-card :cover="smartTravel1" class="swiper-image" @click="onClick">
						<!-- <image slot='cover' style="width: 100%;" :src="cover"></image> -->
						<text class="uni-body">山川壮丽——让我们徒步远足探索自然奇观。</text>
						<view slot="actions" class="card-actions card-actions-flex">
							<view class="card-actions-item" @click="actionsClick('分享')">
								<uni-icons type="redo" size="18" color="#999"></uni-icons>
								<text class="card-actions-item-text">分享</text>
							</view>
							<view class="card-actions-item" @click="actionsClick('点赞')">
								<uni-icons type="heart" size="18" color="#999"></uni-icons>
								<text class="card-actions-item-text">点赞</text>
							</view>
							<view class="card-actions-item" @click="actionsClick('评论')">
								<uni-icons type="chatbubble" size="18" color="#999"></uni-icons>
								<text class="card-actions-item-text">评论</text>
							</view>
						</view>
					</uni-card>
		</uni-section>
		<uni-section title="卡片封面图+操作栏" type="line">
					<uni-card :cover="smartTravel3" class="swiper-image" @click="onClick">
						<!-- <image slot='cover' style="width: 100%;" :src="cover"></image> -->
						<text class="uni-body">古城探秘：步入历史的回廊。</text>
						<view slot="actions" class="card-actions card-actions-flex">
							<view class="card-actions-item" @click="actionsClick('分享')">
								<uni-icons type="redo" size="18" color="#999"></uni-icons>
								<text class="card-actions-item-text">分享</text>
							</view>
							<view class="card-actions-item" @click="actionsClick('点赞')">
								<uni-icons type="heart" size="18" color="#999"></uni-icons>
								<text class="card-actions-item-text">点赞</text>
							</view>
							<view class="card-actions-item" @click="actionsClick('评论')">
								<uni-icons type="chatbubble" size="18" color="#999"></uni-icons>
								<text class="card-actions-item-text">评论</text>
							</view>
						</view>
					</uni-card>
		</uni-section>
		<uni-section title="卡片封面图+操作栏" type="line">
					<uni-card :cover="smartTravel2" class="swiper-image" @click="onClick">
						<!-- <image slot='cover' style="width: 100%;" :src="cover"></image> -->
						<text class="uni-body">这个夏天去哪里？不如让我们一起享受阳光沙滩和清澈海水！</text>
						<view slot="actions" class="card-actions card-actions-flex">
							<view class="card-actions-item" @click="actionsClick('分享')">
								<uni-icons type="redo" size="18" color="#999"></uni-icons>
								<text class="card-actions-item-text">分享</text>
							</view>
							<view class="card-actions-item" @click="actionsClick('点赞')">
								<uni-icons type="heart" size="18" color="#999"></uni-icons>
								<text class="card-actions-item-text">点赞</text>
							</view>
							<view class="card-actions-item" @click="actionsClick('评论')">
								<uni-icons type="chatbubble" size="18" color="#999"></uni-icons>
								<text class="card-actions-item-text">评论</text>
							</view>
						</view>
					</uni-card>
		</uni-section>
	</view>
</template>

<script>
export default {
    data() {
        return {
            background: ['color1', 'color2', 'color3'],
            indicatorDots: true,
            autoplay: true,
            interval: 2000,
            duration: 500,
			smartTravel1: '../../../../static/icon/pic1.jpg',
			smartTravel2: '../../../../static/icon/pic2.jpg',
			smartTravel3: '../../../../static/icon/oldTown.png',
			cover: 'https://web-assets.dcloud.net.cn/unidoc/zh/shuijiao.jpg',
			avatar: 'https://web-assets.dcloud.net.cn/unidoc/zh/unicloudlogo.png',
			
        }
    },
    methods: {
		onClick(e){
			console.log(e)
		},
		actionsClick(text){
			uni.showToast({
				title:text,
				icon:'none'
				})
		},
        changeIndicatorDots(e) {
            this.indicatorDots = !this.indicatorDots
        },
        changeAutoplay(e) {
            this.autoplay = !this.autoplay
        },
        intervalChange(e) {
            this.interval = e.target.value
        },
        durationChange(e) {
            this.duration = e.target.value
        }
    }
}
</script>


<style lang="less" scoped>
	.swiper-image{
		width: 100%;
		height: 100%;
		object-fit: contain;
	}
	.card-actions {
	  display: flex;
	  justify-content: space-between;
	}
	.card-actions-item {
	  flex: 1;
	  display: flex;
	  align-items: center;
	  justify-content: center;
	  flex-direction: column;
	}
	/* .card-actions{
			flex-flow: row;
			justify-content: flex-start;
			display: flex;
			width: 100%
		} */
	.uni-margin-wrap {
		width: 690rpx;
		width: 100%;
	}
	.swiper {
		height: 300rpx;
	}
	.swiper-item {
		display: block;
		height: 300rpx;
		line-height: 300rpx;
		text-align: center;
	}
	.swiper-list {
		margin-top: 40rpx;
		margin-bottom: 0;
	}
	.uni-common-mt {
		margin-top: 60rpx;
		position: relative;
	}
	.info {
		position: absolute;
		right: 20rpx;
	}
	.uni-padding-wrap {
		width: 550rpx;
		padding: 0 100rpx;
	}
</style>
