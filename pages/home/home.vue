<template>
	<view>
		<nav-bar backState="2000" title="首页"></nav-bar>
		<!-- 公共组件-每个页面必须引入 -->
		<public-module></public-module>
	</view>
</template>

<script>
import { sha256 } from 'js-sha256'

export default {
	data() {
		return {
			
		};
	},
	onLoad(e) {
		
	},
	onShow() {
		this.httpTest()
	},
	//方法
	methods: {
		onPageJump(url) {
			uni.navigateTo({
				url: url
			});
		},
		httpTest() {
			var time = Math.round(new Date().getTime()/1000).toString();
			var params={
			    'accessKey':'11111',
			    'secretKey':'22222',
			    'timestamp':time,
			};
			var str=""
			//忽略了排序
			for(var i in params){
				str+=i+params[i]
			}
			var sign = sha256(str) //要加密的密码
			//请求数据
			this.$http.post(
				`demo/index/index/?accessKey=11111&secretKey=22222&timestamp=${time}&sign=${sign}`,
				{},
				{ load: false },
			).then(data => {
				console.log(data)
			});
		}
	},
	//页面下来刷新
	onPullDownRefresh() {},
	//页面上拉触底
	onReachBottom() {},
	//用户点击分享
	onShareAppMessage(e) {
		return this.wxShare();
	}
};
</script>
<style lang="scss" scoped>
@import '@/style/mixin.scss';
</style>
