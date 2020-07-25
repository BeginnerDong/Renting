<template>
	<view class="font-26 line-h px-3">
		
		<view class="flex1 py-4 bB-f5" v-for="(v,i) in 5" @click="change(i)">
			<view>
				<view class="d-flex a-end pb-3">
					<view class="font-30 pr-3">中华世纪城智能柜机</view>
					<view>15968246857</view>
				</view>
				<view class="color6">西安市雁塔区高新科技路西段239号中华世纪城</view>
			</view>
			<image src="../../static/images/the problem-icon1.png" class="wh32" v-if="changeCurr==i"></image>
			<image src="../../static/images/the problem-icon2.png" class="wh32" v-else></image>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				changeCurr:0
			}
		},
		methods: {
			change(i){
				const self = this;
				self.changeCurr = i
			}
		}
	}
</script>

<style>

</style>
