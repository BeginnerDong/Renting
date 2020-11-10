<template>
	<view>
		
		<!-- banner -->
		<view class="banner p-r">
			<swiper :indicator-dots="false" :autoplay="true" :interval="3000" :duration="1000" @change="swiper">
				<block v-for="(item,index) in mainData.bannerImg" :key="index">
					<swiper-item>
							<image :src="item.url" ></image>
					</swiper-item>
				</block>
			</swiper>
			
			<view class="font-22 colorf p-a bannerTag">{{current}}/{{mainData.bannerImg.length}}</view>
		</view>
		
		<view class="radius20-T bg-white pt-3 line-h p-r content">
			<view class="pb-4 bB-e1 mx-3">
				<view class="colorR font-26"><text class="font-36">{{mainData.price}}</text> 元/月</view>
				<view class="font-32 pt-2 pb-3">{{mainData.title}} {{mainData.layout}}</view>
				<view class="font-22 color9 flex1">
					<view>房源编号：{{mainData.description}}</view>
					<view>更新时间：{{mainData.create_time}}</view>
				</view>
			</view>
			
			<!-- 租房展示 -->
			<view class="flex2 py-4 bB-e1 mx-3" v-if="mainData.menu_id==1">
				<view class="flex4">
					<view>{{mainData.orientation}}</view>
					<view class="font-22 color9 pt-2">朝向</view>
				</view>
				<view class="flex4">
					<view>{{mainData.area}}㎡</view>
					<view class="font-22 color9 pt-2">面积</view>
				</view>
				<view class="flex4">
					<view>{{mainData.floor}}</view>
					<view class="font-22 color9 pt-2">楼层</view>
				</view>
				<view class="flex4">
					<view>{{mainData.renovation}}</view>
					<view class="font-22 color9 pt-2">装修</view>
				</view>
			</view>
			<!-- 二手、车位、办公展示 -->
			<view class="flex2 py-4 bB-e1 mx-3 font-22" v-else>
				<view class="flex4">
					<view class="font-32 colorR font-w pb-2">{{mainData.price}}元/月</view>
					<view>售价</view>
				</view>
				<!-- 二手展示 -->
				<view class="flex4" v-show="mainData.menu_id==2">
					<view class="font-32 colorR font-w pb-2">黄雁村</view>
					<view>位置</view>
				</view>
				<!-- 办公展示 -->
				<view class="flex4" v-show="mainData.menu_id==3">
					<view class="font-32 colorR font-w pb-2">{{mainData.layout}}</view>
					<view>房型</view>
				</view>
				
				<view class="flex4">
					<view class="font-32 colorR font-w pb-2">{{mainData.area}}㎡</view>
					<view>建筑面积</view>
				</view>
				<!-- 车位展示 -->
				<view class="flex4" v-show="mainData.menu_id==4">
					<view class="font-32 colorR font-w pb-2">地下停车场</view>
					<view>类型</view>
				</view>
			</view>
			
			
			
			<view class="pb-4 font-26 p-r mx-3">
				<view class="flex pt-4" v-show="mainData.menu_id==1">
					<view class="tag pb-1" v-for="(item,index) in mainData.tagList" :key="index">{{item.title}}</view>
				</view>
				<view>
					<view class="flex1 flex-wrap" v-show="mainData.menu_id==1||mainData.menu_id==4">
						<view class="w-50 pt-4" v-show="mainData.menu_id==4"><text class="color6">单价：</text>{{mainData.unit_price}}/㎡/天</view>
						<view class="w-50 pt-4" v-show="mainData.menu_id==4"><text class="color6">区域：</text>{{mainData.region}}</view>
						<view class="w-50 pt-4" v-show="mainData.menu_id==1"><text class="color6">付款：</text>{{mainData.pay_type}}</view>
						<view class="w-50 pt-4" v-show="mainData.menu_id==1"><text class="color6">电梯：</text>{{mainData.elevator}}</view>
						<view class="w-50 pt-4"><text class="color6">小区：</text>{{mainData.village}}</view>
						
						<view class="flex colorM pt-4" @click="Router.navigateTo({route:{path:'/pages/detail-estate/detail-estate?id='+mainData.id}})">
							<view>查看小区</view>
							<image src="../../static/images/the-problem-icon3.png" class="R-icon ml-1"></image>
						</view>
					</view>
					
					<view class="flex1 flex-wrap" v-show="mainData.menu_id==2||mainData.menu_id==3">
						<view class="w-50 pt-4" v-show="mainData.menu_id==3"><text class="color6">楼层：</text>{{mainData.unit_price}}</view>
						<view class="w-50 pt-4" v-show="mainData.menu_id==3"><text class="color6">区域：</text>{{mainData.region}}</view>
						<view class="w-50 pt-4" v-show="mainData.menu_id==3"><text class="color6">工位：</text>{{mainData.station}}</view>
						<view class="w-50 pt-4" v-show="mainData.menu_id==3"><text class="color6">位置：</text>{{mainData.location}}</view>
						<view class="w-50 pt-4" v-show="mainData.menu_id==2"><text class="color6">单价：</text>{{mainData.unit_price}}</view>
						<view class="w-50 pt-4" v-show="mainData.menu_id==2"><text class="color6">挂牌：</text>{{mainData.show_time}}</view>
						<view class="w-50 pt-4" v-show="mainData.menu_id==2"><text class="color6">朝向：</text>{{mainData.orientation}}</view>
						<view class="w-50 pt-4" v-show="mainData.menu_id==2"><text class="color6">楼层：</text>{{mainData.floor}}</view>
						<view class="w-50 pt-4"><text class="color6">楼型：</text>{{mainData.building_type}}</view>
						<view class="w-50 pt-4"><text class="color6">电梯：</text>{{mainData.elevator}}</view>
						<view class="w-50 pt-4"><text class="color6">装修：</text>{{mainData.renovation}}</view>
						<view class="w-50 pt-4"><text class="color6">年代：</text>{{mainData.years}}</view>
						<view class="w-50 pt-4"><text class="color6">用途：</text>{{mainData.purpose}}</view>
						<view class="w-50 pt-4"><text class="color6">权属：</text>{{mainData.ownership}}</view>
						<view class="w-50 pt-4"><text class="color6">小区：</text>{{mainData.village}}</view>
						
						<view class="flex colorM pt-4" @click="Router.navigateTo({route:{path:'/pages/detail-estate/detail-estate?id='+mainData.id}})">
							<view>查看小区</view>
							<image src="../../static/images/the-problem-icon3.png" class="R-icon ml-1"></image>
						</view>
					</view>
					
				</view>
			</view>
			<view class="h20"></view>
			
			<!-- 房屋配置(只有租房的房源详情展示) -->
			<view v-if="mainData.menu_id==1">
				<view class="mx-3 py-4 font-24 pzBox">
					<view class="font-32 font-w">房屋配置</view>
					<view class="flex flex-wrap">
						<block v-for="(item,index) in disposeData" :key="index">
							<view class="flex4 w-20 pt-4">
								<image :src="item.state?item.url[1]:item.url[0]"></image>
								<view :class="item.state?'':'colorB line-through'">{{item.title}}</view>
							</view>
						</block>
					</view>
				</view>
				<view class="h20"></view>
			</view>
			
			<!-- 房屋维护人 -->
			<view class="mx-3 py-4">
				<view class="font-32 font-w">房屋维护人</view>
				<view class="flex1 pt-3">
					<image :src="mainData.headImg[0].url" class="wh80 radius-5"></image>
					<view class="flex-1 pl-2">
						<view>{{mainData.contact}}</view>
						<view class="font-24 color6 pt-2">{{mainData.shop}}</view>
					</view>
					<image src="../../static/images/details-icon.png" class="dh-icon" @click="callPhone"></image>
				</view>
			</view>
			<view class="h20"></view>
			
			<!-- 位置及周边 -->
			<view class="pt-4">
				<view class="font-32 font-w px-3">位置及周边</view>
				<view class="position pt-3 p-r">
					<image :src="mainData.addressImg[0].url" ></image>
					<view class="pName font-26 p-aXY m-a">
						<image src="../../static/images/details-icon1.png"></image>
						<view class="p-aXY">{{mainData.village}}</view>
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
				<view class="flex4 pl-5 pr-2" @click="save">
					<image src="../../static/images/details-icon4.png" class="wh32 mb-1" v-if="isCollect"></image>
					<image src="../../static/images/details-icon3.png" class="wh32 mb-1" v-else></image>
					<view>收藏</view>
				</view>
				<button class="flex4 pl-5 pr-2" open-type="share">
					<image src="../../static/images/details-icon2.png" class="wh30 mb-1"></image>
					<view>分享</view>
				</button>
			</view>
			<view class="zxBtn" @click="callPhone">电话咨询</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				disposeData:[
					{'url':['../../static/images/details-icon5.png','../../static/images/details-icon6.png'],'title':'电视'},
					{'url':['../../static/images/details-icon7.png','../../static/images/details-icon8.png'],'title':'冰箱'},
					{'url':['../../static/images/details-icon9.png','../../static/images/details-icon10.png'],'title':'洗衣机'},
					{'url':['../../static/images/details-icon11.png','../../static/images/details-icon12.png'],'title':'空调'},
					{'url':['../../static/images/details-icon13.png','../../static/images/details-icon14.png'],'title':'热水器'},
					{'url':['../../static/images/details-icon17.png','../../static/images/details-icon18.png'],'title':'暖气'},
					{'url':['../../static/images/details-icon15.png','../../static/images/details-icon16.png'],'title':'床'},
					{'url':['../../static/images/details-icon19.png','../../static/images/details-icon20.png'],'title':'WIFI'},
					{'url':['../../static/images/details-icon21.png','../../static/images/details-icon22.png'],'title':'衣柜'},
					{'url':['../../static/images/details-icon23.png','../../static/images/details-icon24.png'],'title':'燃气灶'},
					{'url':['../../static/images/details-icon26.png','../../static/images/details-icon25.png'],'title':'沙发'},
					{'url':['../../static/images/details-icon28.png','../../static/images/details-icon27.png'],'title':'桌椅'},
					{'url':['../../static/images/details-icon30.png','../../static/images/details-icon29.png'],'title':'油烟机'},
					{'url':['../../static/images/details-icon32.png','../../static/images/details-icon31.png'],'title':'电磁炉'},
					{'url':['../../static/images/details-icon34.png','../../static/images/details-icon33.png'],'title':'微波炉'},
				],
				mainData:{},
				current:1,
				collectData:[],
				isCollect:false
			}
		},
		onLoad(){
			const self = this;
			if(uni.getStorageSync('rentDetail')){
				self.mainData = uni.getStorageSync('rentDetail')
				console.log('rentDetail',self.mainData)
				self.facilities(self.mainData.facilitiesList)
			};
			console.log('self.isCollect',self.isCollect)
			self.isCollect = self.$Utils.getStorageArray('collectData', 'id', self.mainData.id);
			if(self.isCollect){
				if(self.isCollect.length <= 0 ){
					self.isCollect = false
				}
			}
			console.log('self.isCollect2',self.isCollect)
		},
		methods: {
			
			callPhone(){
				const self = this;
				uni.makePhoneCall({
				  phoneNumber: self.mainData.phone, 
					success: (res) => {
						console.log('调用成功!')	
					},
					fail: (res) => {
						console.log('调用失败!')
					}
				});
			},
			
			save(){
				const self = this;
				console.log('self.isCollect',self.isCollect)
				
				if(self.isCollect){
					self.$Utils.delStorageArray('collectData','id', self.mainData.id);
					self.isCollect = false;
					self.$Utils.showToast('取消收藏','none')
				}else{
					self.$Utils.setStorageArray('collectData',self.mainData, 'id', 99999999);
					self.isCollect = true;
					self.$Utils.showToast('收藏成功','none')
				}
				
			},
			
			swiper(e){
				const self = this;
				// console.log(e.target.current+1)
				self.current = e.target.current + 1;
			},
			
			//判断房屋内设备
			facilities(list){
				const self = this;
				for(var i=0; i<self.disposeData.length;i++){
					for(var j=0; j<list.length; j++){
						if(self.disposeData[i].title == list[j].title){
							self.disposeData[i].state = true;
						}
					}
				}
			}
			
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

button{font-size: 24rpx;line-height: 1;background-color: #fff;color: #666;}
</style>
