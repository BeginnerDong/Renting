<template>
	<view>
		
		<view class="px-3">
			<view class="p-r flex py-3">
				<image src="../../static/images/home-icon1.png" class="ss-icon ml-2"></image>
				<input type="text" v-model="title" placeholder="请输入小区名/完整房源编号" />
				<view class="colorM font-30" @click="getMainData(true)">搜索</view>
			</view>
			
			<!-- <view class="yx py-3 bB-e1 flex1" v-for="v in 4" :key="v" @click="Router.navigateTo({route:{path:'/pages/detail/detail'}})">
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
			</view> -->
			
			<view class="yx py-3 bB-f5 flex1" v-for="(item,index) in mainData"  :key="index"
			@click="goDetail(item)">
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
			
			
			
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router,
				mainData:[],
				isLoadAll:false,
				title:'',
				searchItem:{
					user_no:''
				}
			}
		},
		onLoad(option){
			const self = this;
			self.searchItem.user_no = uni.getStorageSync('shopData').user_no;
			self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
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
			
			search(){
				const self = this;
				self.getMainData(true)
			},
			
			getMainData(isNew) {
				const self = this;
				const postData = {};
				if (isNew) {
					self.mainData = [];
					self.paginate = self.$Utils.cloneForm(self.$AssetsConfig.paginate);
				};
				postData.title = self.title;
				postData.searchItem = self.$Utils.cloneForm(self.searchItem);
				postData.paginate = self.$Utils.cloneForm(self.paginate);
				postData.getAfter = {
				 	tagList:{
				 		tableName:'Label',
				 		middleKey:'tag',
				 		key:'id',
						condition:'in'
					}
				}
				var callback = function(res){
					if(res.info.data.length > 0){
						self.mainData = res.info.data;
					}else{
						self.isLoadAll = true;
					};
					console.log('mainData',res)
					self.$Utils.finishFunc('getMainData');
				}
				self.$apis.searchInfo(postData, callback);
			},
		}
	}
</script>
<style>
page{background-color: #f5f5f5;}
</style>
<style scoped>

</style>
