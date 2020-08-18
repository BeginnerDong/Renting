<template>
	<view>
		
		
		<view class="px-3">
			<view class="flex1 py-2">
				<view class="flex" @click="Router.navigateTo({route:{path:'/pages/store/store'}})">
					<view>{{shopData.name}}</view>
					<image src="../../static/images/classification-icon.png" class="sj-icon"></image>
				</view>
				<view class="p-r flex bg-f5 p-2 ss" @click="Router.navigateTo({route:{path:'/pages/search/search'}})">
					<image src="../../static/images/home-icon1.png" class="ss-icon"></image>
					<input type="text" value="" placeholder="请输入小区名/完整房源编号" />
				</view>
			</view>
			
			<!-- banner -->
			<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000" indicator-active-color="#fff">
				<block v-for="(item,index) in bannerData" :key="index">
					<swiper-item>
							<image :src="item.mainImg[0].url" ></image>
					</swiper-item>
				</block>
			</swiper>
			
			<!-- 金刚区 -->
			<view class="flex2 line-h font-26 my-4">
				<view class="flex4" @click="Router.navigateTo({route:{path:'/pages/classify/classify?id=1'}})">
					<image src="../../static/images/home-icon2.png" class="wh100 mb-2"></image>
					<view>租房</view>
				</view>
				<view class="flex4" @click="Router.navigateTo({route:{path:'/pages/classify/classify?id=2'}})">
					<image src="../../static/images/home-icon3.png" class="wh100 mb-2"></image>
					<view>二手房</view>
				</view>
				<view class="flex4" @click="Router.navigateTo({route:{path:'/pages/classify/classify?id=3'}})">
					<image src="../../static/images/home-icon4.png" class="wh100 mb-2"></image>
					<view>办公</view>
				</view>
				<view class="flex4" @click="Router.navigateTo({route:{path:'/pages/classify/classify?id=4'}})">
					<image src="../../static/images/home-icon5.png" class="wh100 mb-2"></image>
					<view>车位</view>
				</view>
			</view>
			
			<!-- 热门 -->
			<view class="font-34 font-w pt-2 pb-3">热门推荐</view>
			<view class="flex1">
				<block v-for="(item,index) in hotData"  :key="index">
					<view class="p-r radius10 overflow-h mb-3 hot" v-show="index<4"
					@click="Router.navigateTo({route:{path:'/pages/hot/hot'}})">
						<image :src="item.mainImg[0].url" class="hotImg"></image>
						<view class="colorf font-30 p-a bottom-0 w-100 p-2 avoidOverflow hotTxt">{{item.title}}</view>
					</view>
				</block>
			</view>
			
			
			<!-- 优选房源 -->
			<view class="font-34 font-w pt-2">优选房源</view>
			<view class="yx py-3 bB-f5 flex1" v-for="(item,index) in excellentData"  :key="index" 
			@click="goDetail(item)">
				<image :src="item.mainImg[0].url" class="yxImg"></image>
				<view class="line-h flex5 pl-2 flex-1 yxTxt">
					<view class="font-30">{{item.title}}</view>
					<view class="font-24 colorS">{{item.area}}/㎡ {{item.layout}}</view>
					<view class="flex flex-wrap">
						<view class="tag" v-for="(c_item,c_index) in item.tagList" :key="c_index" v-show="c_index<4">{{c_item.title}}</view>
					</view>
					<view class="priceY">{{item.price}}</view>
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
				mainData:[],
				bannerData:{},
				hotData:[],
				excellentData:[],
				shopData:{}
			}
		},
		onLoad() {
			const self = this;
			if(uni.getStorageSync('shopData')){
				self.getBannerData();
				self.getMainData(true)
			}else{
				self.$Utils.loadAll(['getBannerData','getLocation'], self);
			}
			self.shopData = uni.getStorageSync('shopData');
			// self.getLocation();
		},
		onShow() {
			const self = this;
			if(uni.getStorageSync('changeShop')){
				self.shopData = uni.getStorageSync('shopData');
				self.getMainData(true);
			};
		},
		methods: {
			
			getLocation(){
				const self = this;
				console.log('经纬度')
				uni.getLocation({
					type:'wgs84',
					success(res) {
						self.getShopData(res.longitude,res.latitude)
						console.log('经纬度',res.longitude,res.latitude)
					},
					fail(res){
						console.log('fail',res)
						setTimeout(function(){
							self.$Utils.showToast('检查您的定位是否打开', 'none')
						},2000)
						self.getShopData(0,0)
						self.$Utils.finishFunc('getLocation');
					}
				})
			},
			
			getShopData(longitude,latitude) {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					user_type: 1
				};
				postData.order = {
					distance:'asc',
					longitude:longitude,
					latitude:latitude
				};
				var callback = function(res){
					if(res.info.data.length > 0){
						self.shopData = res.info.data[0];
						uni.setStorageSync('shopData',res.info.data[0]);
					};
					self.getMainData();
					console.log("shopData",self.shopData)
					
				}
				self.$apis.userInfoGet(postData, callback);
			},
			
			goDetail(item){
				const self = this;
				uni.setStorageSync('rentDetail',item)
				self.Router.navigateTo({route:{path:'/pages/detail/detail'}});
			},
			

			
			getBannerData() {
				const self = this;
				const postData = {};
				// postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					thirdapp_id: 2,
					menu_id: 8
				};
				var callback = function(res){
					if(res.info.data.length > 0){
						self.bannerData = res.info.data
					}
					// console.log('banner',self.bannerData)
					self.$Utils.finishFunc('getBannerData');
				}
				self.$apis.articleGet(postData, callback);
			},
			
			getMainData(isNew) {
				const self = this;
				
				if (isNew) {
					self.mainData = [];
					self.excellentData = [];
					self.hotData = [];
					// self.paginate = {
					// 	count: 0,
					// 	currentPage: 1,
					// 	is_page: true,
					// 	pagesize: 10
					// }
				};
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					// menu_id: 1,
					thirdapp_id: 2,
					user_type: 1,
					user_no:uni.getStorageSync('shopData').user_no
				};
				postData.getAfter = {
				 	tagList:{
				 		tableName:'Label',
				 		middleKey:'tag',
				 		key:'id',
						condition:'in'
					},
					facilitiesList:{
						tableName:'Label',
						middleKey:'facilities',
						key:'id',
						condition:'in'
					}
				}
				var callback = function(res){
					if(res.info.data.length > 0){
						self.mainData = res.info.data;
						for (var i = 0; i < self.mainData.length; i++) {
							if(self.mainData[i].excellent == 1){
								 self.excellentData.push(self.mainData[i])
							}
							if(self.mainData[i].hot == 1){
								self.hotData.push(self.mainData[i])
							}
						}
					};
					uni.removeStorageSync('changeShop');
					self.$Utils.finishFunc('getLocation');
				}
				self.$apis.articleGet(postData, callback);
			},
			
			
			
		}
	};
</script>
<style scoped>
.ss{width: 500rpx;height: 66rpx;border-radius: 33rpx;}
swiper,swiper-item{width: 690rpx;height: 320rpx;border-radius: 10rpx;overflow: hidden;}

.hot{width: 335rpx;height: 210rpx;}
.hotTxt{background-image: linear-gradient(to bottom, rgba(0,0,0,0), rgba(0,0,0,0.7));text-align: center;}

</style>