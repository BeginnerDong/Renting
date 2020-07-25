<template>
	<view>
		
		<view class="flex1 mx-3 py-3 bB-f5" v-for="(v,i) in 5" :key="i" @click="Router.navigateTo({route:{path:'/pages/user-submitQuestion/user-submitQuestion'}})">
			<view class="flex-1 pl-2">无法打开小程序</view>
			<image src="../../static/images/the problem-icon3.png" class="R-icon"></image>
		</view>
		
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

</style>
