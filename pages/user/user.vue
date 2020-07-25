<template>
	<view>
		
		<view class="headBox">
			<view class="font-36 head":style="{paddingTop:statusBar+'px'}">我的</view>
			<view class="flex font-32 font-w py-4 px-3">
				<image src="../../static/images/my-img.png" class="wh110 mr-2"></image>
				<view>哆啦A梦</view>
			</view>
		</view>
		
		<view class="flex1 px-2 bg-white mb-2 radius10 mx-3 py-3" @click="Router.navigateTo({route:{path:'/pages/user-collection/user-collection'}})">
			<image src="../../static/images/my-icon1.png" class="start-icon"></image>
			<view class="flex-1 pl-2">我的收藏</view>
			<image src="../../static/images/the problem-icon3.png" class="R-icon"></image>
		</view>
		
		<view class="bg-white mb-2 radius10 mx-3">
			<view class="flex1 mx-2 py-3 bB-e1" @click="Router.navigateTo({route:{path:'/pages/user-question/user-question'}})">
				<image src="../../static/images/my-icon2.png" class="start-icon"></image>
				<view class="flex-1 pl-2">反馈问题</view>
				<image src="../../static/images/the problem-icon3.png" class="R-icon"></image>
			</view>
			<view class="flex1 mx-2 py-3" @click="Router.navigateTo({route:{path:'/pages/aboutUS/aboutUS'}})">
				<image src="../../static/images/my-icon.png" class="start-icon"></image>
				<view class="flex-1 pl-2">关于我们与帮助</view>
				<image src="../../static/images/the problem-icon3.png" class="R-icon"></image>
			</view>
		</view>
		
		
		
		
		
		<view style="height: 130rpx;"></view>
		<!-- footer -->
		<view class="footer">
			<view class="item" @click="Router.redirectTo({route:{path:'/pages/index/index'}})">
				<image src="../../static/images/nabar.png" mode=""></image>
				<view>首页</view>
			</view>
			<view class="item on">
				<image src="../../static/images/nabar2-a.png" mode=""></image>
				<view>我的</view>
			</view>
		</view>
		
		
		
	</view>
</template>

<script>
	const app = getApp();
	export default {
		data() {
			return {
				Router:this.$Router,
				statusBar: app.globalData.statusBar
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
.headBox{background-image: linear-gradient(to bottom,#B0DFFF,#f5f5f5);}
.head{line-height: 100rpx;text-align: center;}
</style>
