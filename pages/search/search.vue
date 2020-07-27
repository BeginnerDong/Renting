<template>
	<view>
		
		<view class="px-3">
			<view class="p-r flex py-3">
				<image src="../../static/images/home-icon1.png" class="ss-icon ml-2"></image>
				<input type="text" value="" placeholder="请输入小区名/完整房源编号" />
				<view class="colorM font-30">搜索</view>
			</view>
			
			<view class="yx py-3 bB-e1 flex1" v-for="v in 4" :key="v" @click="Router.navigateTo({route:{path:'/pages/detail/detail'}})">
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
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				Router:this.$Router
			}
		},
		methods: {
			
		}
	}
</script>
<style>
page{background-color: #f5f5f5;}
</style>
<style scoped>

</style>
