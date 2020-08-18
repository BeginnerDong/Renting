<template>
	<view>
		
		<view class="p-3">
			<view class="pt-4"><text class="color6">建筑年代：</text>{{mainData.years}}</view>
			<view class="pt-4"><text class="color6">建筑类型：</text>{{mainData.building_type}}</view>
			<view class="pt-4"><text class="color6">房屋总数：</text>{{mainData.building_num}}</view>
			<view class="pt-4"><text class="color6">物业公司：</text>{{mainData.property}}</view>
			<view class="pt-4"><text class="color6">物业费：</text>{{mainData.property_fee}}</view>
			<view class="pt-4"><text class="color6">开发商：</text>{{mainData.developer}}</view>
			<view class="pt-4"><text class="color6">小区地址：</text>{{mainData.address}}</view>
			<view class="pt-4"><text class="color6">小区名：</text>{{mainData.village}}</view>
			<view class="pt-4" v-show="mainData.menu_id==2"><text class="color6">二手房价：</text><text class="priceM">{{mainData.second_price}}</text></view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				mainData:{}
			}
		},
		onLoad(){
			const self = this;
			self.mainData = uni.getStorageSync('rentDetail')
		},
		methods: {
			
		}
	}
</script>

<style>

</style>
