<template>
	<view>
		
		<!-- banner -->
		<view class="banner p-r">
			<swiper :indicator-dots="false" :autoplay="true" :interval="3000" :duration="1000">
				<swiper-item>
						<image src="../../static/images/details-img.png" ></image>
				</swiper-item>
			</swiper>
			
			<view class="font-22 colorf p-a bannerTag">1/5</view>
		</view>
		
		<view class="radius20-T bg-white pt-3 line-h p-r content">
			<view class="pb-4 bB-e1 mx-3">
				<view class="colorR font-26"><text class="font-36">1400</text> 元/月</view>
				<view class="font-32 pt-2 pb-3">单间·康源小区 3室0厅3卫</view>
				<view class="font-22 color9 flex1">
					<view>房源编号：102000566</view>
					<view>更新时间：2020.07.23 15:23:09</view>
				</view>
			</view>
			
			<!-- 租房展示 -->
			<!-- <view class="flex2 py-4 bB-e1 mx-3">
				<view class="flex4">
					<view>东</view>
					<view class="font-22 color9 pt-2">朝向</view>
				</view>
				<view class="flex4">
					<view>20㎡</view>
					<view class="font-22 color9 pt-2">面积</view>
				</view>
				<view class="flex4">
					<view>低楼层/34层</view>
					<view class="font-22 color9 pt-2">楼层</view>
				</view>
				<view class="flex4">
					<view>精装</view>
					<view class="font-22 color9 pt-2">装修</view>
				</view>
			</view> -->
			<!-- 二手、车位、办公展示 -->
			<view class="flex2 py-4 bB-e1 mx-3 font-22">
				<view class="flex4">
					<view class="font-32 colorR font-w pb-2">9562元/月</view>
					<view>售价</view>
				</view>
				<!-- 二手展示 -->
				<view class="flex4">
					<view class="font-32 colorR font-w pb-2">黄雁村</view>
					<view>位置</view>
				</view>
				<!-- 办公展示 -->
				<!-- <view class="flex4">
					<view class="font-32 colorR font-w pb-2">3室两厅</view>
					<view>房型</view>
				</view> -->
				
				<view class="flex4">
					<view class="font-32 colorR font-w pb-2">20㎡</view>
					<view>建筑面积</view>
				</view>
				<!-- 车位展示 -->
				<!-- <view class="flex4">
					<view class="font-32 colorR font-w pb-2">地下停车场</view>
					<view>类型</view>
				</view> -->
			</view>
			
			
			
			<view class="py-4 font-26 p-r mx-3">
				<view class="flex">
					<view class="tag tagB pb-1">优选好房</view>
					<view class="tag tagO pb-1">拎包入住</view>
				</view>
				<view class="flex1 flex-wrap">
					<view class="w-50 pt-4"><text class="color6">付款：</text>押一付三</view>
					<view class="w-50 pt-4"><text class="color6">电梯：</text>有</view>
					<view class="w-50 pt-4"><text class="color6">小区：</text>康园小区</view>
					
					<view class="flex colorM pt-4" @click="Router.navigateTo({route:{path:'/pages/detail-estate/detail-estate'}})">
						<view>查看小区</view>
						<image src="../../static/images/the problem-icon3.png" class="R-icon ml-1"></image>
					</view>
				</view>
			</view>
			<view class="h20"></view>
			
			<!-- 房屋配置(之后租房的房源详情展示) -->
			<view>
				<view class="mx-3 py-4 font-24 pzBox">
					<view class="font-32 font-w">房屋配置</view>
					<view class="flex flex-wrap">
						<view class="flex4 w-20 pt-4" v-for="(v,i) in disposeData" :key="i">
							<image :src="v.state?v.url[1]:v.url[0]"></image>
							<view :class="v.state?'':'colorB line-through'">{{v.title}}</view>
						</view>
					</view>
				</view>
				<view class="h20"></view>
			</view>
			
			<!-- 房屋维护人 -->
			<view class="mx-3 py-4">
				<view class="font-32 font-w">房源维护人</view>
				<view class="flex1 pt-3">
					<image src="../../static/images/details-img1.png" class="wh80"></image>
					<view class="flex-1 pl-2">
						<view>芦荟</view>
						<view class="font-24 color6 pt-2">鲁光科技原点</view>
					</view>
					<image src="../../static/images/details-icon.png" class="dh-icon"></image>
				</view>
			</view>
			<view class="h20"></view>
			
			<!-- 位置及周边 -->
			<view class="pt-4">
				<view class="font-32 font-w px-3">位置及周边</view>
				<view class="position pt-3 p-r">
					<image src="../../static/images/details-img2.png" ></image>
					<view class="pName font-26 p-aXY m-a">
						<image src="../../static/images/details-icon1.png"></image>
						<view class="p-aXY">康园小区</view>
					</view>
					<view class="font-26 colorf p-aX flex2 pBto">
						<view>地铁</view>
						<view>公交</view>
						<view>餐饮</view>
						<view>银行</view>
						<view>医院</view>
						<view>学校</view>
					</view>
				</view>
			</view>
			
		</view>
		
		
		<view style="height: 100rpx;"></view>
		<view class="flex1 p-fX bottom-0 bg-white bT-e1">
			<view class="font-24 color6 flex flex-1">
				<view class="flex4 pl-5 pr-2">
					<image src="../../static/images/details-icon3.png" class="wh32 mb-1"></image>
					<view>收藏</view>
				</view>
				<view class="flex4 pl-5 pr-2">
					<image src="../../static/images/details-icon2.png" class="wh30 mb-1"></image>
					<view>分享</view>
				</view>
			</view>
			<view class="zxBtn">电话咨询</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				disposeData:[
					{'url':['../../static/images/details-icon5.png','../../static/images/details-icon6.png'],'title':'电视','state':false},
					{'url':['../../static/images/details-icon7.png','../../static/images/details-icon8.png'],'title':'冰箱','state':true},
					{'url':['../../static/images/details-icon9.png','../../static/images/details-icon10.png'],'title':'洗衣机','state':false},
					{'url':['../../static/images/details-icon11.png','../../static/images/details-icon12.png'],'title':'空调','state':false},
					{'url':['../../static/images/details-icon13.png','../../static/images/details-icon14.png'],'title':'热水器','state':true},
					{'url':['../../static/images/details-icon17.png','../../static/images/details-icon18.png'],'title':'暖气','state':true},
					{'url':['../../static/images/details-icon15.png','../../static/images/details-icon16.png'],'title':'床','state':true}
				]
			}
		},
		methods: {
			
		}
	}
</script>

<style scoped>
swiper,swiper-item{width: 100%;height: 550rpx;}
.bannerTag{width: 70rpx;line-height: 32rpx;text-align: center;background-color: rgba(0,0,0,0.7);border-radius: 16rpx;right: 30rpx;bottom: 50rpx;}

.content{margin-top: -30rpx;}

.h20{background-color: #F5F9FC;height: 20rpx;}
.colorB{color: #bbb;}

.pzBox image{width: 70rpx;height: 60rpx;margin-bottom: 20rpx;}
.w-20{width: 20%;}
.dh-icon{width: 44rpx;height: 56rpx;}
.position{width: 100%;height: 480rpx;}
.pName{width: 180rpx;height: 90rpx;line-height: 90rpx;text-align: center;}
.pBto{bottom: 0;background-color: rgba(0,0,0,0.5);line-height: 80rpx;}
.zxBtn{line-height: 100rpx;background-color: #2BA5FA;width: 260rpx;color: #fff;text-align: center;}
</style>
