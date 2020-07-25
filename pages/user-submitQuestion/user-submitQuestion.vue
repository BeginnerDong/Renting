<template>
	<view class="px-3">
		
		<view class="py-3 bB-e1">无法打开小程序</view>
		<view class="font-24 color9 py-3 bB-e1">
			<textarea value="" placeholder="请填写10个字以上的问题以便我们提供更好的帮助" />
			<view class="text-right">0/200</view>
		</view>
		<view class="py-3 bB-e1">
			<view>截图（0/4）</view>
			<view class="flex">
				<image src="../../static/images/the problem-icon.png" class="wh120 mt-3 mr-3"></image>
			</view>
		</view>
		<view class="py-3 bB-e1 flex1 mb-2">
			<view>联系方式</view>
			<input type="text" value="" placeholder="邮箱/手机号" class="flex-1 ml-3" />
		</view>
		
		<view class="flex0 font-24 color6 pt-5 mt-5">
			<!-- <image src="../../static/images/the problem-icon1.png" class="wh28 mr-1"></image> -->
			<image src="../../static/images/the problem-icon2.png" class="wh28 mr-1"></image>
			<view>允许开发者48小时内通过客服消息联系我</view>
		</view>
		<view class="btnAuto">提交</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			}
		},
		methods: {
			
		}
	}
</script>

<style>
page{background-color: #fff;}
.btnAuto{width: 400rpx;margin-top: 20rpx;}
</style>
