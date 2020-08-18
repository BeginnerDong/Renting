<template>
	<view class="px-3">
		
		<view class="py-3 bB-e1">{{title}}</view>
		<view class="font-24 color9 py-3 bB-e1">
			<textarea maxlength="200" value="" v-model="submitData.content" placeholder="请填写10个字以上的问题以便我们提供更好的帮助" />
			<view class="text-right">{{submitData.content.length}}/200</view>
		</view>
		<view class="py-3 bB-e1">
			<view>截图（{{submitData.mainImg.length}}/4）</view>
			<view class="flex flex-wrap imgBox">
				<image v-for="(item,index) in submitData.mainImg" :key="index" :src="item.url" class="wh120 mt-3 mr-2"></image>
				<image @click="upLoadImg('mainImg')" src="../../static/images/the-problem-icon.png" class="wh120 mt-3 mr-2" v-if="submitData.mainImg.length<4"></image>
			</view>
		</view>
		<view class="py-3 bB-e1 flex1 mb-2">
			<view>联系方式</view>
			<input type="text" value="" v-model="submitData.phone" placeholder="邮箱/手机号" class="flex-1 ml-3" />
		</view>
		
		<view class="flex0 font-24 color6 pt-5 mt-5" @click="Agree">
			<image src="../../static/images/the-problem-icon1.png" class="wh28 mr-1" v-if="agree"></image>
			<image src="../../static/images/the-problem-icon2.png" class="wh28 mr-1" v-else></image>
			<view>允许开发者48小时内通过客服消息联系我</view>
		</view>
		<view class="btnAuto" @click="agreeSubmit">提交</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				agree:false,
				id:-1,
				title:'产品建议',
				submitData:{
					title:'',
					content:'',
					mainImg:[],
					phone:'',
					thirdapp_id:2
				}
			}
		},
		onLoad(option){
			const self = this;
			if(option.id == -1){
				self.title = '产品建议'
			}else{
				self.title = uni.getStorageSync('function').title
			};
			self.$Utils.loadAll(['getUserData'], self);
		},
		methods: {
			
			getUserData() {
				const self = this;
				const postData = {};
				
				postData.tokenFuncName = 'getProjectToken';
				const callback = (res) => {
					if (res.info.data.length > 0) {
						self.userData = res.info.data[0];
						self.userData.info.deadline_change = self.$Utils.timeto(parseInt(self.userData.info.deadline*1000),'ymd-hm')
					}
					self.$Utils.finishFunc('getUserData');
				};
				self.$apis.userGet(postData, callback);
			},
			
			Agree(){
				const self = this;
				self.agree = !self.agree;
				
			},
			
			agreeSubmit(){
				const self = this;
				console.log(self.agree)
				if(self.submitData.content == ''){
					self.$Utils.showToast('请填写您所遇到的问题', 'none')
				}else if(self.submitData.phone == ''){
					self.$Utils.showToast('请填写联系方式', 'none')
				}else if(self.agree){
					self.$Utils.showToast('请允许客服人员联系您', 'none')
				}else{
					self.submit()
				}
			},
			
			submit(){
				const self = this;
				self.submitData.title = self.title;
				const postData = {
					data:self.submitData
				};
				postData.tokenFuncName = 'getProjectToken';
				const callback = (res) => {
					
					uni.setStorageSync('canClick', true);
					if (res.solely_code == 100000) {
						uni.showToast({
						    title: '提交成功',
						    duration: 2000,
						});
						setTimeout(function(){
							uni.navigateBack({
							    delta: 1
							});
						},2000);
					} else {
						self.$Utils.showToast('网络故障', 'none')
					};
				};
				self.$apis.messageAdd(postData, callback);
			},
			
			upLoadImg(type) {
				const self = this;			
				
				const callback = (res) => {
					console.log('res', res)
					if (res.solely_code == 100000) {
						self.submitData[type].push({url:res.info.url,type:'image'})
					}else {
						self.$Utils.showToast('网络故障', 'none')
					}
				};				
				uni.chooseImage({
					count: 1,
					success: function(res) {
						console.log(res);
						var tempFilePaths = res.tempFilePaths[0];
						var file = res.tempFiles[0];
						var obj = res.tempFiles[0].path.lastIndexOf(".");
						var ext = res.tempFiles[0].path.substr(obj+1);
						console.log(callback)
						console.log('img',self.submitData)
						self.$Utils.uploadFile(tempFilePaths, 'file', {
							tokenFuncName: 'getProjectToken',ext:ext,md5:'md5',totalSize:file.size,start:0,chunkSize:file.size,originName:'headImg'
						}, callback)
					},
					fail: function(err) {
						uni.hideLoading();
					},			
				})			
			},
			
		}
	}
</script>

<style>
page{background-color: #fff;}
.btnAuto{width: 400rpx;margin-top: 20rpx;}
textarea{color: #222;width: 100%;}
.imgBox image:nth-child(5){margin-right: 0;}
</style>
