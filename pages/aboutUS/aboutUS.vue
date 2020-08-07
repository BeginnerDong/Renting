<template>
	<view>
		
		<view class="flex1 py-3 mx-3 bB-f5">
			<image src="../../static/images/about us-icon1.png" class="wh50"></image>
			<view class="color6 flex-1 pl-2">客服信息</view>
			<view class="font-26">{{mainData.description}}</view>
		</view>
		<view class="flex1 py-3 mx-3 bB-f5">
			<image src="../../static/images/about us-icon.png" class="wh50"></image>
			<view class="color6 flex-1 pl-2">联系电话</view>
			<view class="font-26">{{mainData.phone}}</view>
		</view>
		<view class="f5Bj-H20"></view>
		
		<view class="p-3 content">
			<view class="content ql-editor" style="padding:0;" v-html="mainData.content">
				
			</view>
			<image src="../../static/images/about us-img.png" mode="widthFix"></image>
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
			self.$Utils.loadAll(['getMainData'], self);
		},
		methods: {
			
			getMainData() {
				const self = this;
				const postData = {};
				// postData.tokenFuncName = 'getProjectToken';
				postData.searchItem = {
					menu_id: 5,
					thirdapp_id: 2
				};
				var callback = function(res){
					if(res.info.data.length > 0){
						self.mainData = res.info.data[0];
					}
					console.log('mainData',self.mainData)
					self.$Utils.finishFunc('getMainData');
				}
				self.$apis.articleGet(postData, callback);
			}
			
		}
	}
</script>

<style scoped>
.content image{margin-top: 30rpx;width: 100%;height: 400rpx;}
</style>
