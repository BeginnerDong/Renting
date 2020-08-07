<template>
	<view>
		
		<view class="list">
			<view class="li" :class="liCurr==1?'on':''" @click="changeLi(1)">租房</view>
			<view class="li" :class="liCurr==2?'on':''" @click="changeLi(2)">二手房</view>
			<view class="li" :class="liCurr==3?'on':''" @click="changeLi(3)">办公</view>
			<view class="li" :class="liCurr==4?'on':''" @click="changeLi(4)">车位</view>
		</view>
		
		
		<block v-for="(item,index) in mainData"  :key="index" @click="goDetail(item)">
			<view class="yx mx-3 py-3 bB-f5 flex1" v-show="item.menu_id==liCurr">
				<image :src="item.mainImg[0].url" class="yxImg"></image>
				<view class="line-h flex5 pl-2 flex-1 yxTxt">
					<view class="font-30">{{item.title}}</view>
					<view class="font-24 colorS">{{item.area}}/㎡ {{item.layout}}</view>
					<view class="flex">
						<view class="tag" v-for="(c_item,c_index) in item.tagList" :key="c_index">{{c_item.title}}</view>
					</view>
					<view class="priceY">{{item.price}}</view>
				</view>
			</view>
		</block>
		
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				liCurr:1,
				mainData:[]
			}
		},
		onLoad(){
			const self = this;
			self.mainData = self.$Utils.getStorageArray('collectData');
			console.log('self.mainData',self.mainData);
		},
		methods: {
			changeLi(i){
				const self = this;
				self.liCurr = i
			},
			
			goDetail(item){
				const self = this;
				uni.setStorageSync('rentDetail',item)
				self.Router.navigateTo({route:{path:'/pages/detail/detail'}});
			},
			
			
		}
	}
</script>

<style>
.li{width: 25%;}
</style>
