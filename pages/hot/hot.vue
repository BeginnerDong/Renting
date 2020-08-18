<template>
	<view>
		
		<view class="px-3">
			
			<view class="yx py-3 bB-f5 flex1" v-for="(item,index) in mainData"  :key="index"
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
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				mainData:[],
				isLoadAll:false
			}
		},
		onLoad() {
			const self = this;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
			self.$Utils.loadAll(['getMainData'], self);
		},
		onReachBottom(){
			const self = this;
			if(!self.isLoadAll){
				self.paginate.currentPage++;
				self.getMainData(true);
			};
		},
		methods: {
			
			goDetail(item){
				const self = this;
				uni.setStorageSync('rentDetail',item)
				self.Router.navigateTo({route:{path:'/pages/detail/detail'}});
			},
			
			getMainData(isNew) {
				const self = this;
				if (isNew) {
					self.mainData = [];
					self.paginate = {
						count: 0,
						currentPage: 1,
						is_page: true,
						pagesize: 10
					}
				};
				const postData = {};
				postData.tokenFuncName = 'getProjectToken';
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.searchItem = {
					thirdapp_id: 2,
					user_type: 1,
					user_no:uni.getStorageSync('shopData').user_no,
					hot:1
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
						self.mainData.push.apply(self.mainData,res.info.data)
						
					}else{
						self.isLoadAll = true
					};
					console.log('mainData',self.mainData)
					self.$Utils.finishFunc('getMainData');
				}
				self.$apis.articleGet(postData, callback);
			},
			
		}
	}
</script>

<style>

</style>
