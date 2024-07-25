<template>
	<view>
		<view style="margin-top: 40rpx;margin-left: 16rpx;color:red;">
			当前经纬度：{{latitude}} ，{{longitude}}
			<!-- {{marker[0].latitude}} {{marker[0].longitude}} -->
		</view>
		<div class="inputData">
			<!-- label>起始地点: </label> -->
			<input type="text" v-model="startLocation" placeholder="请输入起始地点">
			<input  type="text" v-model="endLocation" placeholder="请输入目的地点">
		</div>
		<button style="min-height: 30px;" @click="callShowLatLanAndRoute(startLocation,endLocation)">SEARCH</button>
		<!-- <button style="min-height: 30px;" @click="showLatitudeAndLongitude(startLocation)">SEARCH</button> -->
		<button style="min-height: 30px;" @click="test">TEST</button>
		
		
		<map class="map" :latitude="latitude" :longitude="longitude" :markers="marker" :scale='scale'
			:controls="controls" :circles="circles" :polyline="polyline">
		</map>

	</view>
</template>




<script>
	import QQMapWX from "../../jsFile/qqmap-wx-jssdk.js"
	//引入腾旭地图sdk
	// import QQMapWX from '../../untils/qqmap-wx-jssdk.js'
	import app from '../../App.vue'
	// 引入uni-map-common公共模块
	// const UniMap = require('uni-map-common');
	// 初始化实例
	// let uniMap = new UniMap({
	// 	provider: "qqmap", // 指定使用哪家地图供应商
	// 	key: "J6OBZ-53Y3Z-DP4XL-ZCAOT-2HITE-C4BDE"
	// });
	
	// console.log("result", result);
	export default {
		data() {
			return {
				title: 'Hello index',
				latitude: null,
				longitude: null,
				// 初始化起点终点 名称
				startLocation:"",
				endLocation:"",
				
				// 起点经纬度
				startLatitude:0.0,
				startLongitude:0.0,
				// 终点经纬度
				endLongitude:0.0,
				endLatitude:0.0,
				
				// 蒙版地标位置
				marker: [{
					id: 0,
					latitude: null, //经度
					longitude: null, //纬度
					iconPath: '../../static/img/location3.png', //显示的图标
					rotate: 0, // 旋转度数
					width: 40, //宽
					height: 40, //高
					title: '你在哪了', //标注点名
					alpha: 0.5, //透明
				}, ],
			}
		},
		onLoad() {
			//拿地址
			this.getMapAddress();
		},
		methods: {
			// planRouteByLocation(){
			// 	// 调用API
			// 	let result = await uniMap.route({
			// 		mode: "driving",
			// 		from: "40.034852,116.319820",
			// 		to: "39.771075,116.351395",
			// 	})
			// 	console.log("新的路线规划result：", result)
			// },
			// 调用两次路径解析 并且调用路线规划
			
			showLatitudeAndLongitude(position,flag){
				uni.request({
				    url: 'https://restapi.amap.com/v3/geocode/geo?parameters',
				     method: 'GET',
				    data: {
				     key: 'ce64420c0d4dd1c70ebbe71363d60e6d', //高德地图key
				     address:position// 详细地址
				    },
				    success: (res) => {
				     console.log("打印地址解析结果", res)
				     let lo = res.data.geocodes[0].location.split(',')[0]
				     let la = res.data.geocodes[0].location.split(',')[1]
				     // console.log('经纬度',la,"隔离",lo)
					 // console.log(typeof(this.startLatitude),la)
					 if (flag){
						 this.startLatitude = la
						 this.startLongitude = lo
					 }
					 else{
						 this.endLatitude = la
						 this.endLongitude = lo
					 }
				    }
				   })

			},
			testCallShowLatLanAndRoute(){
				console.log("打印经纬度查看")
				console.log("起点经纬度",this.startLatitude,this.startLongitude)
				console.log("终点经纬度",this.endLatitude,this.endLongitude)
			},
			// 传入起点终点对象，调用函数进行解析
			roadRoute(startPoint,endPoint){
				console.log("打印起点",startPoint,"打印终点",endPoint)
				// 路线规划 测试方法
				let plugin = requirePlugin('routePlan');
				let key = 'J6OBZ-53Y3Z-DP4XL-ZCAOT-2HITE-C4BDE';  //使用在腾讯位置服务申请的key
				let referer = '智游行智能旅途';   //调用插件的app的名称
				const str='plugin://routePlan/index?key=' + key + '&referer=' + referer + '&endPoint=' + endPoint + '&navigation=1';
				console.log("地址是："+str);
				uni.navigateTo({
					url: str
				})
				
			},
			callShowLatLanAndRoute(startPosition,endPosition){
				console.log("输入起止点",startPosition,endPosition)
				// 要把行末逗号删除
				// 解析起点终点的经纬度
				this.showLatitudeAndLongitude(this.startLocation,true)
				this.showLatitudeAndLongitude(this.endLocation,false)
				this.testCallShowLatLanAndRoute()
				// 定义startPoint endPoint
				var startPoint  = JSON.stringify({
						'name': '起点',
						'latitude': this.startLatitude,
						'longitude': this.startLongitude
				});
				var endPoint = JSON.stringify({  //终点
						'name': '终点',
						'latitude': this.endLatitude,
						'longitude': this.endLongitude
				});
				// 传入对象 调用路线规划
				this.roadRoute(startPoint,endPoint)
				// 最后打印经纬度
				this.testCallShowLatLanAndRoute()
			},
			test(){
				// 路线规划 测试方法
				let plugin = requirePlugin('routePlan');
				let key = 'J6OBZ-53Y3Z-DP4XL-ZCAOT-2HITE-C4BDE';  //使用在腾讯位置服务申请的key
				let referer = '智游行智能旅途';   //调用插件的app的名称
				let endPoint = JSON.stringify({  //终点
						'name': '北京西站',
						'latitude': 39.894806,
						'longitude': 116.321592
				});
				let startPoint  =JSON.stringify({
						'name': '北京西站',
						'latitude': 39.894806,
						'longitude': 116.321592
				})
				const str='plugin://routePlan/index?key=' + key + '&referer=' + referer + '&endPoint=' + endPoint + '&navigation=1';
				console.log("地址是："+str);
				uni.navigateTo({
					url: str
				})
				
			},
			getMapAddress() {
				const tMap = new QQMapWX({
					key: '4DABZ-MTZ2R-PZLW2-WX6FG-W5IXE-APFAF' //开发者密钥
				});

				//使用 uni.getLocation获取用户所在经纬度
				uni.getLocation({
					type: 'wgs84',   //加密方式 gcj02
					geocode: true,
					// altitude: true,
					isHighAccuracy:true,  //这个高精度配置好像没什么用
					success: (res) => {
						console.log("获取经纬度成功",res);
						this.latitude = res.latitude;
						this.longitude = res.longitude;
						this.marker[0].latitude = res.latitude;
						this.marker[0].longitude = res.longitude;
					},
					fail: () => {
						console.log("获取经纬度失败");
					},
					complete: () => {
						// 使用腾讯sdk的reverseGeocoder方法 解析经纬度
						tMap.reverseGeocoder({
							location: {
								latitude: this.latitude,
								longitude: this.longitude
							},
							success: function(res) {
								console.log("解析地址成功", res);
								console.log("当前地址：", res.result.address);
								//保存缓存
								uni.setStorage({
									key: 'local',
									data: res.result.address,
									success() {
										console.log("用户地址信息已缓存")
									}
								})
							},
							fail: function(res) {
								uni.showToast({
									title: '定位失败',
									duration: 2000,
									icon: "none"
								})
								console.log(res);
							},
							complete: function(res) { //无论成功失败都会执行
								wx.switchTab({
									url: '../appointment/appointment'
								})
							}
						})
					}
				})
			},
			doNavi() {
				let plugin = requirePlugin('routePlan');
				let key = 'J6OBZ-53Y3Z-DP4XL-ZCAOT-2HITE-C4BDE'; //使用在腾讯位置服务申请的key
				let referer = '智游行智能旅途推荐系统'; //调用插件的app的名称
				let startPoint = JSON.stringify({ //终点
					'name': '湖南省湘西土家族苗族自治州吉首市世纪大道',
					'latitude': 36.66826,
					'longitude': 117.02076
				});
				let endPoint = JSON.stringify({ //终点
					'name': '青岛大学',
					latitude: 36.10061184894021,
					longitude: 120.45523630249923
				});
				uni.navigateTo({
					url: 'plugin://routePlan/index?key=' + key + '&referer=' + referer + '&endPoint=' + endPoint +
						'&startPoint=' + startPoint + '&navigation=1',
					success(res) {
						console.log("res==1111=", res)
					},
					fail(res) {
						console.log("res==2222=", res)
					},
				});
			}
		},
	}
</script>

<style lang="less" scoped>
	.inputData {
		display: flex;
		justify-content: space-between;
		max-height: 30px;
	}

	.search-result {
		padding-top: 10px;
		padding-bottom: 20px;
		text-align: center;
	}

	.search-result-text {
		text-align: center;
		font-size: 14px;
		color: #666;
	}

	.example-body {
		/* #ifndef APP-NVUE */
		display: block;
		/* #endif */
		padding: 0px;
	}

	.uni-mt-10 {
		margin-top: 10px;
	}

	.map {
		height: 100vh;
		width: 100vw;
	}
</style>
