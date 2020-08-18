<template>
	<view class="font-26 line-h px-3">
		
		<view class="flex1 py-4 bB-f5" v-for="(item,index) in mainData" :key="index" 
		@click="change(item,index)">
			<view>
				<view class="d-flex a-end pb-3">
					<view class="font-30 pr-3">{{item.name}}</view>
					<view>{{item.phone}}</view>
				</view>
				<view class="color6">{{item.address}}</view>
			</view>
			<image src="../../static/images/the-problem-icon1.png" class="wh32" v-if="user_no==item.user_no"></image>
			<image src="../../static/images/the-problem-icon2.png" class="wh32" v-else></image>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				changeCurr:0,
				mainData:[],
				user_no:''
			}
		},
		onLoad(){
			const self = this;
			self.user_no = uni.getStorageSync('shopData').user_no;
			self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			change(item,i){
				const self = this;
				self.changeCurr = i;
				
				uni.setStorageSync('shopData',item);
				uni.setStorageSync('changeShop',true);
				uni.navigateBack({
				    delta: 1
				});
			},
			
			getMainData() {
				const self = this;
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					user_type: 1
				};
				var callback = function(res){
					if(res.info.data.length > 0){
						self.mainData = res.info.data;
					}
					console.log("mainData",self.mainData)
					self.$Utils.finishFunc('getMainData');
				}
				self.$apis.userInfoGet(postData, callback);
			}
			
		}
	}
</script>

<style>

</style>
