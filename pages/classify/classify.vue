<template>
	<view>
		
		
		<view class="z100">
			<view class="px-3 pt-2 bg-white">
				<view class="p-r flex bg-f5 z100 ss">
					<image src="../../static/images/home-icon1.png" class="ss-icon ml-2"></image>
					<input type="text" value="" placeholder="请输入小区名/完整房源编号" />
				</view>
			</view>
			
			
			<view class="p-r z100 bg-white">
				<view class="fon-30 p-3 flex1">
					<view class="flex0 w140" :class="liCurr==0?'colorM':''" @click="changeLi(0)">
						<view>租房</view>
						<image src="../../static/images/classification-icon1.png" class="sj-icon" v-if="liCurr==0"></image>
						<image src="../../static/images/classification-icon.png" class="sj-icon" v-else></image>
					</view>
					<view class="flex0 w140" :class="liCurr==1?'colorM':''" @click="changeLi(1)">
						<view>价格</view>
						<image src="../../static/images/classification-icon1.png" class="sj-icon" v-if="liCurr==1"></image>
						<image src="../../static/images/classification-icon.png" class="sj-icon" v-else></image>
					</view>
					<view class="flex0 w140" :class="liCurr==2?'colorM':''" @click="changeLi(2)">
						<view>筛选</view>
						<image src="../../static/images/classification-icon1.png" class="sj-icon" v-if="liCurr==2"></image>
						<image src="../../static/images/classification-icon.png" class="sj-icon" v-else></image>
					</view>
					<view class="flex0 w140" :class="liCurr==3?'colorM':''" @click="changeLi(3)">
						<image src="../../static/images/classification-icon3.png" class="jt-icon" v-if="liCurr==3"></image>
						<image src="../../static/images/classification-icon2.png" class="jt-icon" v-else></image>
					</view>
				</view>
				
				<!-- 点击显示内容 -->
				<view class="p-a left-0 right-0 font-26 radius20-B overflow-h bg-white" v-show="is_show">
					<!-- 分类 -->
					<view class="d-flex" v-show="liCurr==0">
						<view class="left">
							<view class="li" v-for="(v,i) in 4" :key="i" @click="change('left',i)" :class="leftCurr==i?'on':''">不限</view>
						</view>
						<view class="right flex-1 bT-e1">
							<view class="li" v-for="(v,i) in 4" :key="i" @click="change('right',i)">
								<view>不限</view>
								<image src="../../static/images/classification-icon4.png" class="yes-icon" v-show="rightCurr==i"></image>
							</view>
						</view>
					</view>
					<!-- 价钱 -->
					<view class="jiaqian text-center" v-show="liCurr==1">
						<view class="li" v-for="(v,i) in 4" :key="i" @click="change('left',i)" :class="leftCurr==i?'on':''">1000-3000</view>
						
						<view>
							<view class="bg-f5 py-3">3500元-不限</view>
							<view style="height: 100rpx;"></view>
						</view>
						<view class="Mgb colorf py-3">确定</view>
					</view>
					<!-- 筛选 -->
					<view class="bg-mask" style="z-index: 9;" v-show="liCurr==2">
						<view class="choose bg-white p-a right-0 h-100 flex5">
								<view class="flex-1 top">
									<view v-for="v in 5" class="px-3 py-4 bB-e1">
										<view class="pb-1">价格</view>
										<view class="d-flex flex-wrap">
											<view class="oo on">不限</view>
											<view class="oo">3千/月</view>
											<view class="oo">3-5千/月</view>
											<view class="oo">5-8千/月</view>
										</view>
									</view>
								</view>
									
								<view class="flex shadow-lg bto">
									<view class="bg-f5 flex-1" @click="change()">清除</view>
									<view class="Mgb colorf ooBtn">确定</view>
								</view>
						</view>
					</view>
					
					<!-- 其他 -->
					<view class="qita text-center bT-f5" v-show="liCurr==3">
						<view class="p-r" @click="change('qt',0)" :class="qtCurr==0?'bg-f5':''">
							<view class="li">最新发布</view>
							<image src="../../static/images/classification-icon4.png" class="yes-icon p-a right-0 top-0 m-3" v-show="qtCurr==0"></image>
						</view>
						<view class="p-r" @click="change('qt',1)" :class="qtCurr==1?'bg-f5':''">
							<view class="li">价格（从低到高）</view>
							<image src="../../static/images/classification-icon4.png" class="yes-icon p-a right-0 top-0 m-3"  v-show="qtCurr==1"></image>
						</view>
						<view class="p-r" @click="change('qt',2)" :class="qtCurr==2?'bg-f5':''">
							<view class="li">价格（从高到低）</view>
							<image src="../../static/images/classification-icon4.png" class="yes-icon p-a right-0 top-0 m-3"  v-show="qtCurr==2"></image>
						</view>
					</view>
					
				</view>
				
			</view>
			
			
		</view>
		<view class="bg-mask" style="z-index: 9;margin-top: 100rpx;" v-show="is_show && liCurr!=2"></view> 
		
		
		<view class="fon-30 px-3 pb-1 flex flex-wrap">
			<view class="sign">租金月付</view>
			<view class="sign">南北通透</view>
			<view class="sign">交通方便</view>
			<view class="sign">精装</view>
		</view>
		<view class="h20"></view>
		
		
		
		<view class="yx py-3 mx-3 bB-f5 flex1" v-for="v in 4">
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
</template>

<script>
	export default {
		data() {
			return {
				liCurr:0,
				is_show:false,
				rightCurr:0,
				leftCurr:0,
				qtCurr:0
			}
		},
		methods: {
			changeLi(i){
				const self = this;
				if(self.liCurr == i){
					// if(self.is_show)
					self.is_show = !self.is_show
				}else{
					self.is_show = true
				}
				self.liCurr = i
			},
			change(type,i){
				const self = this;
				if(type == 'left'){
					self.leftCurr = i
				}else if(type == 'right'){
					self.rightCurr = i
				}else if(type == 'qt'){
					self.qtCurr = i
				}else{
					self.is_show = false
				}
			}
		}
	}
</script>

<style scoped>
.ss{height: 66rpx;border-radius: 33rpx;}
.w140{width: 140rpx;}
.sign{margin-right: 43rpx;margin-bottom: 20rpx;}
.sign:nth-child(4n){margin-right: 0;}
.h20{height: 20rpx;background-color: #F5F9FC;}

.left{background-color: #f5f5f5;width: 200rpx;border-top: 1px solid #e1e1e1;}
.left .li{line-height: 85rpx;text-align: center;}
.left .on{color: #2BA5FA;position: relative;background-color: #fff;}
.left .on::before{background-color: #2BA5FA;width: 4rpx;height: 85rpx; position: absolute;left: 0;top: 0;content: '';}
.right .li{line-height: 85rpx;box-sizing: border-box;border-bottom: 1px solid #e1e1e1;padding: 0 30rpx;display: flex;justify-content: space-between;align-items: center;}

.jiaqian .li,.qita .li{font-size: 26rpx;padding: 30rpx 0;text-align: center;}

.choose{width: 580rpx;}
.oo{width: 160rpx;line-height: 60rpx;border-radius: 8rpx;margin-right: 23rpx;margin-top: 20rpx;text-align: center;background-color: #f5f5f5;}
.oo:nth-child(3n){margin-right: 0;}
.choose .on{background-color: #2BA5FA;color: #fff;}
.choose .top{overflow-y: scroll;}
.choose .bto{line-height: 80rpx;text-align: center;font-size: 30rpx;}
.ooBtn{width: 420rpx;}
</style>
