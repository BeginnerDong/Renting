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
						<view>{{className[classCurr].name}}</view>
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
					<view v-show="liCurr==0" class="d-flex">
							<view class="left">
								<view class="li" @click="changeClass(item,index)" :class="classCurr==index?'on':''"  v-for="(item,index) in className" :key="index" >
									{{item.name}}
								</view>
							</view>
							<view class="right flex-1 bT-e1">
								<block  v-for="(c_item,c_index) in className[classCurr].con" :key="c_index">
									<view class="li" @click="searchField(className[classCurr].key,c_item,className[classCurr].array[c_index])">
										<view>{{c_item}}</view>
										<image src="../../static/images/classification-icon4.png" class="yes-icon" v-show="searchFieldItem[className[c_index].key]==c_item"></image>
									</view>
								</block>
							</view>
					</view>
					<!-- 价钱 -->
					<view class="jiaqian text-center" v-show="liCurr==1">
						<view class="li" v-for="(item,index) in priceSection" :key="index" @click="selectPrice(item,index)" :class="priceCurr==index?'on':''">{{item}}元</view>
						
						<view>
							<view class="bg-f5 py-3" @click="selectPrice(rangeValues,6)" :class="priceCurr==6?'on':''">
								<text>{{ rangeValues[0] }}</text>~<text>{{ rangeValues[1] }}</text>
							</view>
							<view class="py-3">				<!-- 区域选择 -->
									<RangeSlider
										:width="slideWidth"
										:height="slideHeight"
										:blockSize="slideBlockSize"
										:min="slideMin"
										:max="slideMax"
										:values="rangeValues"
										:step="step"
										:liveMode="isLiveMode"
										@rangechange="onRangeChange"
									>
									</RangeSlider>
							</view>
						</view>
						<view class="Mgb colorf py-3" @click="onPrice(onprice,priceCurr)">确定</view>
					</view>
					<!-- 筛选 -->
					<view class="bg-mask" style="z-index: 9;" v-show="liCurr==2">
						<view class="choose bg-white p-a right-0 h-100 flex5">
								<view class="flex-1 top">
									
									<block  v-for="(item,index) in screen" :key="index">
										<view class="px-3 py-4 bB-e1" v-show="item.type ==1&&classCurr==0">
											<view class="pb-1">{{item.name}}</view>
											<view class="d-flex flex-wrap">
												<view class="oo" v-for="(c_item,c_index) in item.tags" :key="c_index"
												 @click="searchField(item.key,c_item,item.array[c_index])"
												  :class="searchFieldItem[item.key]==c_item?'on':''"
												>{{c_item}}</view>
											</view>
										</view>
									</block>
									
									<block  v-for="(item,index) in screen" :key="index">
										<view class="px-3 py-4 bB-e1" v-show="item.type == classCurr&&classCurr!=0">
											<view class="pb-1">{{item.name}}</view>
											<view class="d-flex flex-wrap">
												<view class="oo" v-for="(c_item,c_index) in item.tags" :key="c_index"
												 @click="searchField(item.key,c_item,item.array[c_index])"
												  :class="searchFieldItem[item.key]==c_item?'on':''"
												>{{c_item}}</view>
											</view>
										</view>
									</block>
									
									<view class="px-3 py-4 bB-e1" v-show="classCurr!=4&&classCurr!=0">
										<view class="pb-1">房源特色</view>
										<view class="d-flex flex-wrap">
											<block v-for="(item,index) in tagData" :key="index">
												<view class="oo" @click="beforeSearch(item.id)" 
												:class="priceCss==item.id?'on':''">{{item.title}}</view>
											</block>
										</view>
									</view>
									
								</view>
									
								<view class="flex shadow-lg bto">
									<view class="bg-f5 flex-1" @click="close">清除</view>
									<view class="Mgb colorf ooBtn" @click="onBefore(priceCss)">确定</view>
								</view>
						</view>
					</view>
					
					<!-- 其他 -->
					<view class="qita text-center bT-f5" v-show="liCurr==3">
						<view class="p-r" @click="change(0)" :class="order.create_time?'bg-f5':''">
							<view class="li">最新发布</view>
							<image src="../../static/images/classification-icon4.png" class="yes-icon p-a right-0 top-0 m-3" v-show="order.create_time"></image>
						</view>
						<view class="p-r" @click="change(1)" :class="order.price=='asc'?'bg-f5':''">
							<view class="li">价格（从低到高）</view>
							<image src="../../static/images/classification-icon4.png" class="yes-icon p-a right-0 top-0 m-3"  v-show="order.price=='asc'"></image>
						</view>
						<view class="p-r" @click="change(2)" :class="order.price=='desc'?'bg-f5':''">
							<view class="li">价格（从高到低）</view>
							<image src="../../static/images/classification-icon4.png" class="yes-icon p-a right-0 top-0 m-3"  v-show="order.price=='desc'"></image>
						</view>
					</view>
					
				</view>
				
			</view>
			
			
		</view>
		<view class="bg-mask" style="z-index: 9;margin-top: 100rpx;" v-show="is_show && liCurr!=2" @click="close"></view> 
		
		
		<view class="fon-30 px-3 pb-1 flex flex-wrap" v-show="classCurr!=0">
			<block v-for="(item,index) in tagData" :key="index">
				<view class="sign">{{item.title}}</view>
			</block>
		</view>
		<view class="h20"></view>
		
		
		
		<view class="yx py-3 mx-3 bB-f5 flex1" v-for="(item,index) in mainData"  :key="index"
		@click="goDetail(item)">
			<image :src="item.mainImg[0].url" class="yxImg"></image>
			<view class="line-h flex5 pl-2 flex-1 yxTxt">
				<view class="font-30">{{item.title}}</view>
				<view class="font-24 colorS">{{item.area}}/㎡ {{item.layout}}</view>
				<view class="flex">
					<view class="tag" v-for="(c_item,c_index) in item.tagList" :key="c_index" >{{c_item.title}}</view>
				</view>
				<view class="priceY">{{item.price}}</view>
			</view>
		</view>
		
		
	</view>
</template>

<script>
	import RangeSlider from '../../components/range-slider/range-slider.vue';
	export default {
		data() {
			return {
				Router:this.$Router,
				liCurr:0,
				is_show:false,
				classCurr:0,
				screen:[
					{name:'装修',tags:['豪装','精装','中装','简装','毛坯'],type:1,key:'renovation',array:[]},
					{name:'付款方式',tags:['押一付三','押一付一','押一付二','半年付','年付','其他'],type:1,key:'pay_type',array:[]},
					{name:'朝向',tags:['东','南','西','北','东南','东北','西南','西北','南北通透'],type:1,key:'orientation',array:[]},
					{name:'价格',tags:['40万以下','40-80万','80-120万','120-150万','150-200万','200万以上'],type:2,key:'price',array:[[0,999999999999],[0,400000],[400000,800000],[800000,1200000],[1200000,1500000],[1500000,2000000],[2000000,9999999999999]]},
					{name:'房型',tags:['一室','两室','三室','四室','五室','五室以上'],type:2,key:'room',array:[]},
					{name:'建筑面积',tags:['50㎡以下','50-80㎡','80-110㎡','110-150㎡','150-200㎡','200㎡以上'],type:2,key:'area',array:[[0,50],[50,80],[80,110],[110,150],[150,200],[200,999999]]},
					{name:'朝向',tags:['东','南','西','北','东南','东北','西南','西北','南北通透'],type:2,key:'orientation',array:[]},
					{name:'价格',tags:['不限','3千/月','3-5千/月','5-8千/月','8千-1万/月','1万/月以上'],type:3,key:'price',array:[[0,99999999999999],[0,3000],[3000,5000],[5000,8000],[8000,10000],[10000,999999999]]},
					{name:'房间',tags:['不限','整栋租赁','带办公家具','整层租赁','独立会议室'],type:3,key:'room',array:[]},
					{name:'建筑面积',tags:['<100㎡','100-300㎡','300-500㎡','500-1000㎡','1000㎡以上'],type:3,key:'area',array:[[0,100],[100,300],[300,500],[500,1000],[1000,999999999]]},
					{name:'装修',tags:['不限','豪华装修','精装修','简单装修','毛坯房'],type:3,key:'renovation',array:[]},
					{name:'类别',tags:['不限','地下','室外'],type:4,key:'ground',array:[]},
					{name:'付款方式',tags:['不限','月付','季付','年付'],type:4,key:'pay_type',array:[]}
				],
				priceSection:['<=800','800~1500','1500~2400','5000~8000','>=8000'],
				className:[
					{name:'不限',con:['不限','1室','2室','3室','4室','公寓'],type:0,key:'room',array:[]},
					{name:'租房',con:['不限','1室','2室','3室','4室','公寓'],type:1,key:'room',array:[]},
					{name:'二手房',con:['不限','1室','2室','3室','4室','公寓'],type:2,key:'room',array:[]},
					{name:'办公',con:['不限','120-150㎡','150-180㎡','180-220㎡','>220㎡','整栋'],type:3,key:'area',array:[[0,9999999999],[120,150],[150,180],[180,220],[220,9999999],'整栋']},
					{name:'车位',con:['不限','室外停车场','地下停车场'],type:4,key:'ground',array:['不限','室外','地下']},
				],
				mainData:[],
				searchItem:{
					thirdapp_id: 2,
					user_type: 1,
					user_no:uni.getStorageSync('shopData').user_no
				},
				searchFieldItem:{
					room:'',           //房间/房型
					orientation:'',     //朝向
					renovation:'',      //装修
					price:'',         //价格
					area:'',      //面积
					ground:'',     //类别
					pay_type:''      //付款方式
				},
				classCurr:0,
				priceCurr:0,
				tagData:[],
				searchItems: {
					thirdapp_id: 2
				},
				priceArray:[
					[0,800],
					[800,1500],
					[1500,2400],
					[5000,8000],
					[8000,999999999999]
				],
				onprice:[],
				
				// 区域选择
				rangeValues: [2000,5000],       //当前区间值
				slideWidth: 570,    //宽度
				slideHeight: 40,     //高度
				slideBlockSize: 30,     //圆形按钮大小
				slideMin: 0,      //slider最小值
				slideMax: 8500,     //slider最大值
				isLiveMode: true,     //是否刷新数值
				step: 100,      //步数
				order:{
					'price':'',
					'create_time':''
				},
				tag:{
				  tableName:'Relation',
				  searchItem:{
						relation_two:''
				  },
				  fixSearchItem:{
				    status:1,
						relation_one_table:'Article',
						relation_two_table:'Label',
				  },
				  key:'relation_one',
				  middleKey:'id',
				  condition:'in',
				},
				priceCss:false,
				getBefore:{}
			}
		},
		components:{
			RangeSlider
		},
		onLoad(option){
			const self = this;
			self.classCurr = option.id;
			self.inPut(option.id)
			self.$Utils.loadAll(['getMainData','getTagData'], self);
		},
		methods: {
			
			
			beforeSearch(id){
			  const self = this;
				if(self.tag.searchItem.relation_two&&self.tag.searchItem.relation_two[1][0]==id){
					self.tag.searchItem.relation_two = '';
					self.getBefore = {};
					self.priceCss =-1
				}else{
					self.tag.searchItem.relation_two = ['in',[id]];
					self.getBefore.tag = self.tag;
					self.priceCss = id
				};
			},
			
			onBefore(id){
				const self = this;
				self.beforeSearch(id)
			  self.getMainData(true);
				self.is_show = false;
			},
			
			change(index){
				const self = this;
				if(index==0){
					self.order.price = "";
					self.order.create_time = "desc";
				}else{
					self.order.price = (index==1?'asc':'desc');
					self.order.create_time = "";
				};
				self.getMainData(true);
				self.is_show = false;
			},
			
			searchField(key,value,array){
				const self = this;
				// console.log('self.searchItem[key]',key);
				// console.log('value',value);
				// console.log('array',array,typeof(array) == 'string')
				if(value&&self.searchItem[key]!=value){
					if(array&&array.length>0){
						if(typeof(array) == 'string'){
							self.searchItem[key] = array;
							self.searchFieldItem[key] = value;
						}else{
							self.searchItem[key] = ['between',array]
							self.searchFieldItem[key] = value;
						}
						self.getMainData(true);
					}else{
						self.searchItem[key] = value;
						self.searchFieldItem[key] = value;
						self.getMainData(true);
					}
				}else if(self.searchItem[key]==value||value=='不限'){
					delete self.searchItem[key];
					self.searchFieldItem[key] = '';
					self.getMainData(true);
				}
				// self.is_show = false;
			},
			
			changeLi(i){
				const self = this;
				if(self.liCurr == i){
					self.is_show = !self.is_show
				}else{
					self.is_show = true
				}
				self.liCurr = i
			},
			
			close(){
				const self = this;
				self.is_show = false
			},
			
			// clear(){
			// 	const self = this;
			// 	for(var i=1;i<self.searchFieldItem.length;i++){
			// 		console.log(self.searchFieldItem.length)
			// 	}
			// 	// self.is_show = false
			// },
			
			goDetail(item){
				const self = this;
				uni.setStorageSync('rentDetail',item)
				self.Router.navigateTo({route:{path:'/pages/detail/detail'}});
			},
			
			inPut(i){
				const self = this;
				if(i == 1){
					self.searchItems.behavior = 1;
					self.searchItems.type = 3;
				}else if(i == 2){
					self.searchItems.type = 4;
					delete self.searchItems.behavior;
				}else if(i == 3){
					self.searchItems.type = 5;
					delete self.searchItems.behavior;
				}else if(i == 0){
					delete self.searchItems.behavior;
					delete self.searchItems.type;
				}
			},
			
			changeClass(item,i){
				const self = this;
				self.classCurr = i;
				self.inPut(i)
				self.getTagData();
				self.getMainData(true);
			},
			
			selectPrice(item,index){
				const self = this;
				self.onprice = item;
				self.priceCurr = index;
				// console.log(index);
				
				if(index>=self.priceArray.length){
					var priceItem = item
				}else{
					var priceItem = self.priceArray[index];
				};
				// console.log(priceItem)
				if(self.searchItem.price&&JSON.stringify(self.searchItem.price[1])==JSON.stringify(priceItem)){
					return;
				};
				self.searchItem.price = ['between',priceItem]
			},
			
			onPrice(item,index){
				const self = this;
				self.selectPrice(item,index);
				self.getMainData(true);
				self.is_show = false;
			},
			
			getTagData(){
				const self = this;
				const postData = {};
				postData.searchItem = self.$Utils.cloneForm(self.searchItems);
				postData.paginate = {
					count: 0,
					currentPage: 1,
					is_page: true,
					pagesize: 4
				};
				var callback = function(res){
					if(res.info.data.length > 0){
						self.tagData = res.info.data;
					}
					// console.log('tagData',self.tagData)
					self.$Utils.finishFunc('getTagData');
				}
				self.$apis.labelGet(postData, callback);
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
				if(self.classCurr != 0){
					self.searchItem.menu_id = self.classCurr;
				}else{
					delete self.searchItem.menu_id
				}
				postData.searchItem = self.$Utils.cloneForm(self.searchItem);
				if(self.order.price){
					postData.order = {
						price:self.order.price
					}
				};
				if(self.order.create_time){
					postData.order = {
						create_time:self.order.create_time
					}
				};
				if(JSON.stringify(self.getBefore) != "{}"){
				  postData.getBefore = self.$Utils.cloneForm(self.getBefore);
				};
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
					}
					// console.log('mainData',res)
					self.$Utils.finishFunc('getMainData');
				}
				self.$apis.articleGet(postData, callback);
			},
			
			// 区域选择滑动事件
			onRangeChange: function(e) {
				this.rangeValues = [e.minValue, e.maxValue];
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
.jiaqian .on{color: #2BA5FA;}

.choose{width: 580rpx;}
.oo{width: 160rpx;line-height: 60rpx;border-radius: 8rpx;margin-right: 23rpx;margin-top: 20rpx;text-align: center;background-color: #f5f5f5;}
.oo:nth-child(3n){margin-right: 0;}
.choose .on{background-color: #2BA5FA;color: #fff;}
.choose .top{overflow-y: scroll;}
.choose .bto{line-height: 80rpx;text-align: center;font-size: 30rpx;}
.ooBtn{width: 420rpx;}
</style>
