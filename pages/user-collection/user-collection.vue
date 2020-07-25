<template>
	<view>
		
		<view class="list">
			<view class="li" :class="liCurr==0?'on':''" @click="changeLi(0)">租房</view>
			<view class="li" :class="liCurr==1?'on':''" @click="changeLi(1)">二手房</view>
			<view class="li" :class="liCurr==2?'on':''" @click="changeLi(2)">办公</view>
			<view class="li" :class="liCurr==3?'on':''" @click="changeLi(3)">车位</view>
		</view>
		
		<view class="yx py-3 mx-3 bB-f5 flex1" v-for="v in 4">
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
</template>

<script>
	export default {
		data() {
			return {
				liCurr:0
			}
		},
		methods: {
			changeLi(i){
				const self = this;
				self.liCurr = i
			}
		}
	}
</script>

<style>
.li{width: 25%;}
</style>
