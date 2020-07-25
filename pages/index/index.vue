<template>
	<view>
		
		
		<view class="px-3">
			<view class="flex1 py-2">
				<view class="flex" @click="Router.navigateTo({route:{path:'/pages/store/store'}})">
					<view>大都荟社区</view>
					<image src="../../static/images/classification-icon.png" class="sj-icon"></image>
				</view>
				<view class="p-r flex bg-f5 p-2 ss" @click="Router.navigateTo({route:{path:'/pages/search/search'}})">
					<image src="../../static/images/home-icon1.png" class="ss-icon"></image>
					<input type="text" value="" placeholder="请输入小区名/完整房源编号" />
				</view>
			</view>
			
			<!-- banner -->
			<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" indicator-active-color="#fff">
				<swiper-item>
						<image src="../../static/images/home-banner.png" ></image>
				</swiper-item>
			</swiper>
			
			<!-- 金刚区 -->
			<view class="flex2 line-h font-26 my-4">
				<view class="flex4" @click="Router.navigateTo({route:{path:'/pages/classify/classify'}})">
					<image src="../../static/images/home-icon2.png" class="wh100 mb-2"></image>
					<view>租房</view>
				</view>
				<view class="flex4" @click="Router.navigateTo({route:{path:'/pages/classify/classify'}})">
					<image src="../../static/images/home-icon3.png" class="wh100 mb-2"></image>
					<view>二手房</view>
				</view>
				<view class="flex4" @click="Router.navigateTo({route:{path:'/pages/classify/classify'}})">
					<image src="../../static/images/home-icon4.png" class="wh100 mb-2"></image>
					<view>办公</view>
				</view>
				<view class="flex4" @click="Router.navigateTo({route:{path:'/pages/classify/classify'}})">
					<image src="../../static/images/home-icon5.png" class="wh100 mb-2"></image>
					<view>车位</view>
				</view>
			</view>
			
			<!-- 热门 -->
			<view class="font-34 font-w pt-2 pb-3">热门推荐</view>
			<view class="flex1">
				<view class="p-r radius10 overflow-h mb-3 hot" v-for="v in 4">
					<image src="../../static/images/home-img.png" class="hotImg"></image>
					<view class="colorf font-30 p-a bottom-0 w-100 py-2 hotTxt">伯顿国际公寓</view>
				</view>
			</view>
			
			
			<!-- 优选房源 -->
			<view class="font-34 font-w pt-2">优选房源</view>
			<view class="yx py-3 bB-f5 flex1" v-for="v in 4" @click="Router.navigateTo({route:{path:'/pages/detail/detail'}})">
				<image src="../../static/images/home-img1.png" class="yxImg"></image>
				<view class="line-h flex5 pl-2 flex-1 yxTxt">
					<view class="font-30">整租·金天地悦睿府</view>
					<view class="font-24 colorS">100/㎡3室2厅1卫</view>
					<view class="flex">
						<view class="tag tagB">优选房源</view>
						<view class="tag tagO">拎包入住</view>
					</view>
					<view class="priceY">3000</view>
				</view>
			</view>
			
			
		</view>
		
		
		
		
		
		<view style="height: 130rpx;"></view>
		<!-- footer -->
		<view class="footer">
			<view class="item on">
				<image src="../../static/images/nabar1-a.png" mode=""></image>
				<view>首页</view>
			</view>
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/user/user'}})">
				<image src="../../static/images/nabar2.png" mode=""></image>
				<view>我的</view>
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				is_show: false,
			}
		},
		onLoad() {
			const self = this;
			// self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			getMainData() {
				const self = this;
				console.log('852369')
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				self.$apis.orderGet(postData, callback);
			}
		}
	};
</script>
<style scoped>
.ss{width: 500rpx;height: 66rpx;border-radius: 33rpx;}
swiper,swiper-item{width: 690rpx;height: 320rpx;border-radius: 10rpx;overflow: hidden;}

.hot{width: 335rpx;height: 210rpx;}
.hotTxt{background-image: linear-gradient(to bottom, rgba(0,0,0,0), rgba(0,0,0,0.7));text-align: center;}

</style>
