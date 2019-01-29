<template>
	<view>
		<view class="header" v-bind:class="{'status':isH5Plus}">
			<view class="userinfo">
				<view class="face"><open-data class="face-pic" type="userAvatarUrl"></open-data></view>
				<view class="info">
					<view class="username">VIP会员<open-data type="userNickName"></open-data></view>
					<view class="integral">积分:{{userinfo.integral}}</view>
				</view>
			</view>
			<view class="setting"><image src="../../static/HM-PersonalCenter/setting.png"></image></view>
		</view>
		<view class="orders">
			<view class="box">
				<view class="label" v-for="(row,index) in orderTypeLise" :key="row.name" hover-class="hover" hover-stay-time="50" @tap="toOrderType(index)">
					<view class="icon"><view class="badge" v-if="row.badge>0">{{row.badge}}</view><image :src="'../../static/HM-PersonalCenter/'+row.icon"></image></view>
					{{row.name}}
				</view>
			</view>
		</view> 
		<view class="list" v-for="(list,list_i) in severList" :key="list">
			<view class="li" v-for="(li,li_i) in list" @tap="toPage(list_i,li_i)" v-bind:class="{'noborder':li_i==list.length-1}"  hover-class="hover"  hover-stay-time="50"  :key="li.name" >
				<view class="icon"><image :src="'../../static/HM-PersonalCenter/sever/'+li.icon"></image></view>
				<view class="text">{{li.name}}</view>
				<image class="to" src="../../static/HM-PersonalCenter/to.png"></image>
			</view>
		</view>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				//#ifdef APP-PLUS
				isH5Plus:true,
				//#endif
				userinfo:{},
				orderTypeLise:[
					//name-标题 icon-图标 badge-角标
					{name:'待付款',icon:'l1.png',badge:1},
					{name:'待发货',icon:'l2.png',badge:2},
					{name:'待收货',icon:'l3.png',badge:6},
					{name:'待评价',icon:'l4.png',badge:9},
					{name:'退换货',icon:'l5.png',badge:0}
				],
				severList:[
					[
						{name:'我的收藏',icon:'point.png'},
						{name:'优惠券',icon:'quan.png'},
						{name:'红包',icon:'momey.png'},
						{name:'任务',icon:'renw.png'},
					],
					[
						{name:'积分明细',icon:'mingxi.png'},
						{name:'抽奖',icon:'choujiang.png'},
						{name:'收货地址',icon:'addr.png'},
						{name:'银行卡',icon:'bank.png'},
						{name:'安全中心',icon:'security.png'},
						{name:"意见反馈",icon:'feedback.png'},
						{name:'在线客服',icon:'kefu.png'}
					]
				],
			};
		},
		onLoad() {
			//加载
			this.init();
		},
		methods: {
			init() {
				//用户信息
				this.userinfo={
					face:'../../static/HM-PersonalCenter/face.jpeg',
					username:"VIP会员10240",
					integral:"1435"
				}		
			},
			//用户点击订单类型
			toOrderType(index){
				uni.showToast({title: this.orderTypeLise[index].name});
			},
			//用户点击列表项
			toPage(list_i,li_i){
				if(this.severList[list_i][li_i].name=="意见反馈"){
					uni.navigateTo({
						url:"../feedback/feedback"
					})
				}
				uni.showToast({title: this.severList[list_i][li_i].name});
			}
		}
	}
</script>

<style lang="scss">
page{background-color:#fff}
.header{
	&.status{padding-top:var(--status-bar-height);}
	background-color:#ff6364;width:92%;height:30vw;padding:0 4%;display:flex;align-items:center;
	.userinfo{
		width:90%;display:flex;
		.face{flex-shrink:0;width:15vw;height:15vw;border-radius:50%;overflow:hidden;
			image,.face-pic{width:100%;height:100%;border-radius:100%;display: inline-block}
		}
		.info{
			display:flex;flex-flow:wrap;padding-left:15px;
			.username{width:100%;color:#fff;font-size:20px}
			.integral{display:flex;align-items:center;padding:0 10px;height:20px;color:#fff;background-color:rgba(0,0,0,0.1);border-radius:10px;font-size:12px}
		}
	}
	.setting{
		flex-shrink:0;width:6vw;height:6vw;
		image{width:100%;height:100%}
	}
}
.hover{background-color:#eee}
.orders{
	background-color:#ff6364;width:92%;height:11vw;padding:0 4%;margin-bottom:calc(11vw + 20px);display:flex;align-items:flex-start;border-radius:0 0 100% 100%;
	.box{
		width:98%;padding:0 1%;height:22vw;background-color:#fefefe;border-radius:12px;box-shadow:0px 0px 10px rgba(0,0,0,0.15);margin-bottom:20px;display:flex;align-items:center;justify-content:center;
		.label{
			display:flex;align-items:center;justify-content:center;flex-flow:wrap;width:100%;height:16vw;color:#666666;font-size:13px;
			.icon{
				position:relative;width:7vw;height:7vw;margin:0 1vw;
				.badge{position:absolute;width:4vw;height:4vw;background-color:#ec6d2c;top:-1vw;right:-1vw;border-radius:100%;font-size:10px;color:#fff;display:flex;align-items:center;justify-content:center}
				image{width:7vw;height:7vw}
			}
		}
	}
}
.list{
	width:100%;border-bottom:solid 13px #f1f1f1;
	.li{
		width:92%;height:50px;padding:0 4%;border-bottom:solid 1px #e7e7e7;display:flex;align-items:center;
	&.noborder{border-bottom:0}
		.icon{
			flex-shrink:0;width:25px;height:25px;
			image{width:25px;height:25px}
		}
		.text{padding-left:10px;width:100%;color:#666}
		.to{flex-shrink:0;width:20px;height:20px}
	}
}
</style>
