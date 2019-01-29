<template>
	<view class="content">
		<!-- <view>
      <text class="title">{{title}}</text>
			<open-data type="userAvatarUrl"></open-data>
			<open-data type="userNickName"></open-data>
			<open-data type="userGender" lang="zh_CN"></open-data>
			<open-data type="userProvince" lang="zh_CN"></open-data>
			<button open-type="getPhoneNumber" bindgetphonenumber="getPhoneNumber">点击获取</button>
    </view> -->
		<view class="uni-padding-wrap">
				<view class="page-section swiper">
						<view class="page-section-spacing">
								<swiper class="swiper" :indicator-dots="indicatorDots" :autoplay="autoplay" :interval="interval" :duration="duration">
										<swiper-item v-for="item in picDate">
												<view class="swiper-item" v-bind:style="{ height: '100%', background:'url(../../static/'+item.pic+')'}"></view>
										</swiper-item>
								</swiper>
						</view>
				</view>
		</view>
		<uni-notice-bar show-icon="true" scrollable="true" show-close="true" speed="50" text="[多行] 这是 NoticeBar 通告栏，这是 NoticeBar 通告栏，这是 NoticeBar 通告栏这是 NoticeBar 通告栏，这是 NoticeBar 通告栏，这是 NoticeBar 通告栏"></uni-notice-bar>
		<uni-grid :data="gridDate" type="rect" showOutBorder="false"></uni-grid>
		<button open-type="contact">进入客服会话</button>
		<button open-type="openSetting">打开授权设置页</button>
	</view>
</template>

<script>
	import uniGrid from "@/components/uni-grid/uni-grid.vue"
	import uniNoticeBar from "@/components/uni-notice-bar/uni-notice-bar.vue"
	export default {
		data() {
			return {
				title: 'Hello',
				indicatorDots: true,
				autoplay: true,
				interval: 2000,
				duration: 500,
				picDate:[
					{pic:'banner.jpg'},{pic:'banner.jpg'},{pic:'banner.jpg'},{pic:'banner.jpg'}
				],
				gridDate:[
					 {image:'https://img-cdn-qiniu.dcloud.net.cn/img/shu.png',text:'圣诞树'},
					{image:'https://img-cdn-qiniu.dcloud.net.cn/img/lindang.png',text:'铃铛'},
					{image:'https://img-cdn-qiniu.dcloud.net.cn/img/laoren.png',text:'圣诞老人'},
					{image:'https://img-cdn-qiniu.dcloud.net.cn/img/liwu.png',text:'礼物'},
					{image:'https://img-cdn-qiniu.dcloud.net.cn/img/maozi.png',text:'帽子'},
					{image:'https://img-cdn-qiniu.dcloud.net.cn/img/shoutao.png',text:'手套'},
					{image:'https://img-cdn-qiniu.dcloud.net.cn/img/xueqiao.png',text:'雪橇'},
					{image:'https://img-cdn-qiniu.dcloud.net.cn/img/xunlu.png',text:'驯鹿'},
					{image:'https://img-cdn-qiniu.dcloud.net.cn/img/xuehua.png',text:'雪花'}
					
				]
			}
		},
		components:{
			uniGrid,
			uniNoticeBar
		},
		onLoad() {

		},
		onReady(){
			console.log("UserInfo")
		},
		methods: {
			getPhoneNumber: function(e) { 
				console.log(e.detail.errMsg,"kkkkkkkkk") 
				console.log(e.detail.iv) 
				console.log(e.detail.encryptedData) 
			},
			loginF(){
				uni.getProvider({
					service: 'oauth',
					success: function(res) {
						console.log(res.provider);
						//支持微信、qq和微博等
						if (~res.provider.indexOf('weixin')) {
							uni.login({
								provider: 'weixin',
								success: function(loginRes) {
									console.log('-------获取openid(unionid)-----');
									console.log(JSON.stringify(loginRes));
									// 获取用户信息
									uni.getUserInfo({
										provider: 'weixin',
										success: function(infoRes) {
											console.log('-------获取微信用户所有-----');
											console.log(JSON.stringify(infoRes.userInfo));
										}
									});
								}
							});
						}
					}
				});
			}
			
		}
	}
</script>

<style>
	.content {
		text-align: center;
		height: 400upx;
	}
    .logo{
        height: 200upx;
        width: 200upx;
        margin-top: 200upx;
    }
	.title {
		font-size: 36upx;
		color: #8f8f94;
	}
</style>
