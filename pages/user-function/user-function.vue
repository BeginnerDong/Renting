<template>
	<view>
		
		<view class="flex1 mx-3 py-3 bB-f5" v-for="(item,index) in mainData" :key="index" @click="goDetail(item)">
			<view class="flex-1 pl-2">{{item.title}}</view>
			<image src="../../static/images/the problem-icon3.png" class="R-icon"></image>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				mainData:[]
			}
		},
		onLoad(){
			const self = this;
			self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			
			goDetail(item){
				const self = this;
				uni.setStorageSync('function',item)
				self.Router.navigateTo({route:{path:'/pages/user-submitQuestion/user-submitQuestion?id='+item.id}});
			},
			
			getMainData() {
				const self = this;
				const postData = {};
				// postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					thirdapp_id: 2,
					type: 2
				};
				var callback = function(res){
					if(res.info.data.length > 0){
						self.mainData = res.info.data;
					}
					self.$Utils.finishFunc('getMainData');
				}
				self.$apis.labelGet(postData, callback);
			}
			
		}
	}
</script>

<style>

</style>
