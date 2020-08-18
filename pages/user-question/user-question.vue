<template>
	<view>
		
		<view class="head mx-3 line-h text-center bB-e1">
			<view class="font-36 font-w">请选择反馈类型</view>
			<view class="font-26 pt-3">你的反馈将发送给小程序开发者</view>
		</view>
		
		<view class="flex1 mx-3 py-3 bB-e1" @click="Router.navigateTo({route:{path:'/pages/user-function/user-function'}})">
			<view class="flex-1 pl-2">功能异常</view>
			<image src="../../static/images/the-problem-icon3.png" class="R-icon"></image>
		</view>
		<view class="flex1 mx-3 py-3 bB-e1" @click="Router.navigateTo({route:{path:'/pages/user-submitQuestion/user-submitQuestion?id=-1'}})">
			<view class="flex-1 pl-2">产品建议</view>
			<image src="../../static/images/the-problem-icon3.png" class="R-icon"></image>
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
.head{padding: 100rpx;}
</style>
