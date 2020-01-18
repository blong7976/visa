<template>
	<view class="content">
		<uni-nav-bar class="navber" left-icon="back" title="我的订单"  fixed backgroundColor="#0db983" color="#fff" :height="height" :top="top" @clickLeft="black">
			<!-- #ifndef MP -->
			<view slot="right" class="rightIcon">
				<image src="../../static/image/icon_service20.png" mode=""></image>
			</view>
			<!-- #endif -->
		</uni-nav-bar>
		
		<view class="navbar">
			<view v-for="(item,index) in navList" :key="index"
				 :class="currentPage===index?'nav-item active':'nav-item'"
				 @click="handleCurrentPage(index)">
				{{item}}
			</view>
		</view>
		
		<swiper @change="changeTab" :current="currentPage"  :style="{height:swiperHeight+'px'}">
			<swiper-item>
				<scroll-view>
					<view class="swiper-body all0">
						<view class="order-item" v-for="(item,index) in orderlist"  :key="index">
							<view class="head">
								<text>订单编号:751423</text>
								<text class="state" v-if="item.state==0">待提交资料</text>
								<text class="state" v-if="item.state==1">待付款</text>
								<text class="state" v-if="item.state==2">已完成</text>
								<text class="state" v-if="item.state==3">退款成功</text>
								<text class="state" v-if="item.state==4">已取消</text>
							</view>
							 <!-- 
							  订单支付后的页面 @click="navTo(`/pages/ShoppingCart/order?type=${item.state}`)"
							  进行中 @click="navTo('/pages/ShoppingCart/orderDetaile')"
							  -->
							<view class="body" @click="routerTo(item)">
								<view class="h1">
									<text class="name">日本一个月单次旅游签证</text>
									<text class="price">100</text>
								</view>
								<view class="h2">
									<text class="laber attr-blue" v-if="item.laber ==0">电子签</text>
									<text class="laber attr-red" v-if="item.laber ==1">贴纸签</text>
									<text class="laber attr-green" v-if="item.laber ==2">另纸签</text>
									<text class="number">1</text>
								</view>
								<view class="h3">
									<text class="date">2019-12-29</text>
									<view class="total">
										共1件商品 合计 <text class="price">100</text>
									</view>
								</view>
							</view>
							<view class="foot">
								<image v-if="item.state==2" src="../../static/image/icon_tpot.png" mode="aspectFit" class="move" @click="move(item,index)"></image>
								<view class="movebox" v-if="item.state==2 && item.move">
									<view @click="delateItem(item,index)">删除订单</view>
								</view>
								
								<view class="btn" v-if="item.state==0">申请退款</view>
								<view class="btn attr-blue" v-if="item.state==0">提交资料</view>
								
								<view class="btn" v-if="item.state==1">取消订单</view>
								<view class="btn attr-blue" v-if="item.state==1" @click="balanceModalShow=true">付款</view>
								
								<view class="btn" v-if="item.state==2">评价</view>
								<view class="btn" v-if="item.state==2">申请开票</view>
								<view class="btn attr-blue" v-if="item.state==2">再次购买</view>
								
								<view class="btn" v-if="item.state==3 || item.state==4">删除订单</view>
								<view class="btn attr-blue" v-if="item.state==3 || item.state==4">再次购买</view>
							</view>
						</view>
					</view>
				</scroll-view>
			</swiper-item>
			<swiper-item>
				<scroll-view>
					<view class="swiper-body all1">
						待付款
					</view>
				</scroll-view>
			</swiper-item>
			<swiper-item>
				<scroll-view>
					<view class="swiper-body all2">
						进行中
					</view>
				</scroll-view>
			</swiper-item>
			<swiper-item>
				<scroll-view>
					<view class="swiper-body all3">
						已完成
					</view>
				</scroll-view>
			</swiper-item>
			<swiper-item>
				<scroll-view>
					<view class="swiper-body all4">
						已取消
					</view>
				</scroll-view>
			</swiper-item>
		</swiper>	
				
				
				
				
		<!-- 支付方式 -->
		<view class="modal share" v-if="playTypeModalShow">
			<view class="modal-dialog ">
				<view class="modal-content">
					<view class="modal-header">
						支付方式
						<image src="../../static/image/icon_close.png" mode="aspectFit" class="close" @click="playTypeModalShow = false"></image>
					</view>
					<view class="modal-body">
						<view class="sharelist" style="padding-bottom: 292upx;">
							<view class="item" @click="selectplayType(0)">
								<view class="left">
									<image src="../../static/image/icon_balance.png" mode="aspectFit"></image>余额支付
									<text class="lb">(￥2986000)</text>
								</view>
								<view class="right">
									<image v-if="playType==0" src="../../static/image/icon_radio_press.png" mode="aspectFit"></image>
									<image v-else src="../../static/image/icon_radio.png" mode="aspectFit"></image>
								</view>
							</view>
							<view class="item" @click="selectplayType(1)">
								<view class="left">
									<image src="../../static/image/icon_wechatpay.png" mode="aspectFit"></image>微信支付
									<text class="lb"></text>
								</view>
								<view class="right">
									<image v-if="playType==1" src="../../static/image/icon_radio_press.png" mode="aspectFit"></image>
									<image v-else src="../../static/image/icon_radio.png" mode="aspectFit"></image>
								</view>
							</view>
							<view class="item" @click="selectplayType(2)">
								<view class="left">
									<image src="../../static/image/icon_alipay.png" mode="aspectFit"></image>支付宝支付
									<text class="lb"></text>
								</view>
								<view class="right">
									<image v-if="playType==2" src="../../static/image/icon_radio_press.png" mode="aspectFit"></image>
									<image v-else src="../../static/image/icon_radio.png" mode="aspectFit"></image>
								</view>
							</view>
						</view>
					</view>
				</view>		
			</view>
		</view>		
				
				
		<!-- 余额支付 确认支付 -->
		<view class="modal share" v-if="balanceModalShow">
			<view class="modal-dialog ">
				<view class="modal-content">
					<view class="modal-header">
						确认付款
						<image src="../../static/image/icon_close.png" mode="aspectFit" class="close" @click="balanceModalShow = false"></image>
					</view>
					<view class="modal-body balance">
						<view class="price">
							<text>600.00</text>
						</view>
						<view class="sharelist">
							<view class="item" >
								<view class="right">
									支付方式
								</view>
								<view class="left" @click="handleSelectplayType">
									<image src="../../static/image/icon_balance.png" mode="aspectFit"></image>余额支付
									<text class="lb">(￥2986000)</text>
								</view>
							</view>
						</view>	
						<view class="btn" @click="balancePlay">
							支付
						</view>
					</view>
				</view>		
			</view>
		</view>		
		
		
		<!-- 余额支付 -> 确认支付 -> 支付密码 -->
		<view class="modal share" v-if="balancePSDModalShow">
			<view class="modal-dialog ">
				<view class="modal-content">
					<view class="modal-header">
						请输入支付密码
						<image src="../../static/image/icon_close.png" mode="aspectFit" class="close" @click="balancePSDModalShow = false"></image>
					</view>
					<view class="modal-body balancepassword">
						<wakary-input type="box" :maxlength='6'></wakary-input>
						<view class="msg" @click="navTo('/pages/login/Retrievepassword')">
							忘记密码？
						</view>
					</view>
				</view>		
			</view>
		</view>				
				
	</view>
</template>

<script>
	import uniNavBar from "@/components/uni-nav-bar/uni-nav-bar.vue";
	import luBarTabNav from "@/components/lu-bar-tab-nav/lu-bar-tab-nav.vue";
	import wakaryInput from '@/components/wakary-input/wakary-input.vue'
	export default{
		components: {uniNavBar,luBarTabNav,wakaryInput},
		data(){
			return{
				top:0,
				height:64,
				navList:["全部","待付款","进行中","已完成","已取消"],
				currentPage:0,
				scrollH: 0, //滚动总高度
				opcity: 0,
				iconOpcity: 0.5,
				listHeight:0,  //内部的高度
				swiperHeight:0,  //外部的高度,
				/** 
				 * 订单状态 state  
				 * 0：待提交资料 
				 * 1：待付款
				 * 2：已完成
				 * 3：退款成功
				 * 4：已取消   
				 * 
				 * 签证类型 laber
				 * 0：电子签   
				 * 1：贴纸签 
				 * 2：另纸签 
				 * **/
				orderlist:[
					{state:0,laber:0,move:false},{state:2,laber:0,move:false},{state:1,laber:1,move:false},{state:2,laber:0,move:false},{state:3,laber:0,move:false},{state:4,laber:2,move:false}
				],
				
				playTypeModalShow:false,
				playType:0,
				balanceModalShow:false,
				balancePSDModalShow:false
			}
		},
		async onLoad(options){
			let obj = {};
			// #ifdef MP-WEIXIN
			obj = wx.getMenuButtonBoundingClientRect();
			// #endif
			// #ifdef MP-BAIDU
			obj = swan.getMenuButtonBoundingClientRect();
			// #endif
			// #ifdef MP-ALIPAY
			my.hideAddToDesktopMenu();
			// #endif
			setTimeout(() => {
				uni.getSystemInfo({
					success: (res) => {
						this.height = obj.top ? (obj.top + obj.height + 8) : (res.statusBarHeight + 44);
						this.top = obj.top ? (obj.top + (obj.height - 32) / 2) : (res.statusBarHeight);
					}
				})
			}, 50)
		},
		onShow() {
			let _this = this;
			setTimeout(function(){
				let list = ".all0";
				_this.getlistHeight(list);
			},10) 
		},
		onPageScroll(e) {
			let scroll = e.scrollTop <= 0 ? 0 : e.scrollTop;
			let opcity = scroll / this.scrollH;
			if (this.opcity >= 1 && opcity >= 1) {
				return;
			}
			this.opcity = opcity;
			this.iconOpcity = 0.5 * (1 - opcity < 0 ? 0 : 1 - opcity)
		},
		methods:{
			navTo(url){
				uni.navigateTo({  
					url
				})  
			},
			black:function() {
				uni.navigateBack()
			},
			handleCurrentPage(index){
				this.currentPage = index
			},
			getlistHeight(list){
				let _this = this
				let info = uni.createSelectorQuery().select(list);
				info.boundingClientRect(function(data) {
					 _this.listHeight = data.height ; // 获取元素高度
					_this.getHeight();
				}).exec();
			},
			getHeight(){
				let _this = this;
				_this.swiperHeight = _this.listHeight;
				return _this.swiperHeight;
			},
			changeTab(e) { 
				let _this = this;
				this.currentPage = e.target.current
				// 不同的tab不同的高度赋不同的值
				if(e.target.current==0){
					let list = ".all0";
					_this.getlistHeight(list);
				}else if(e.target.current==1){
					let list = ".all1";
					_this.getlistHeight(list);
				}else if(e.target.current==2){
					let list = ".all2";
					_this.getlistHeight(list);
				}else if(e.target.current==3){
					let list = ".all3";
					_this.getlistHeight(list);
				}else if(e.target.current==4){
					let list = ".all4";
					_this.getlistHeight(list);
				}
			},
			handlefilter(index){
				let self = this
				this.currentIndex = index
				uni.showLoading({
					title:'加载中',
					complete() {
						setTimeout(()=>{
							self.visatypeList = self.visatypeList.reverse()
							uni.hideLoading()
						},800)
					}
				})
			},
			changeShow(name) {
				this.$refs[name].show();
			},
			confirm(res) {
				this.HSBC = res.data[0].name
			},
			
			move(item,index){
				item.move =! item.move
				this.$set(this.orderlist,index,item)
			},
			delateItem(item,index){
				item.move = false
				this.$set(this.orderlist,index,item)
				this.orderlist.splice(index,index+1)
			},
			selectplayType(e){
				this.playType = e
				this.playTypeModalShow = false
				this.balanceModalShow = true
			},
			handleSelectplayType(){
				this.playTypeModalShow = true
				this.balanceModalShow = false
			},	
			balancePlay(){
				this.balanceModalShow = false
				this.balancePSDModalShow = true
			},
			routerTo(item){
				 // * 订单状态 state  
				 // * 0：待提交资料 
				 // * 1：待付款
				 // * 2：已完成
				 // * 3：退款成功
				 // * 4：已取消   
				 // 订单支付后的页面 @click="navTo(`/pages/ShoppingCart/order?type=${item.state}`)"
				 // 进行中 @click="navTo('/pages/ShoppingCart/orderDetaile')"
				if(item.state==0){
					this.navTo('/pages/ShoppingCart/orderDetaile')
				}else{
					this.navTo(`/pages/ShoppingCart/order?type=${item.state}`)
				}
			}
		}
	}
</script>

<style lang="less" >
	page{
		background: #f7f8fa;padding-bottom: 120upx;
	}
	.yticon{font-size: 24upx;}
	/deep/.uni-navbar__header-btns{
		width: auto;
	}
	.rightIcon{
		position: absolute;
		right: 30upx;
		image{
			width: 45upx;
			height: 45upx;
			float: left;
			padding-right: 20upx;
			&:last-child{
				padding-right: 0;
			}
		}
	}
	
	
	// nav
	.navbar{
		display: flex;
		align-items: center;
		justify-content: space-between;
		height: 85upx;
		line-height: 85upx;
		background: #FFFFFF;
		position: fixed;
		left: 0;
		width: 100%;
		z-index: 999;
		.nav-item{
			flex: 1;
			text-align: center;
			color: #999999;
			font-size: 28upx;
			position: relative;
			&.active{
				color: #333;
			}
			&.active:before{
				position: absolute;
				content: "";
				height: 2px;
				width: 45upx;
				background: #0DB983;
				bottom: 10upx;
				left: 50%;
				transform: translateX(-50%);
			}
		}
	}
	// swiper
	.swiper-body{
		padding:105upx 30upx 0;
		box-sizing: border-box;
	}
	.order-item{
		background: #FFFFFF;
		border-radius: 20upx;
		margin-bottom: 20upx;
		.head{
			height: 80upx;
			line-height: 80upx;
			display: flex;
			justify-content: space-between;
			font-size: 28upx;
			color: #999999;
			padding: 0 30upx;
			border-bottom: 1px solid #ebebeb;
			.state{
				color: #ff7f66;
			}
		}
		.body{
			padding: 20upx 30upx;
			.h1,.h2,.h3{
				display: flex;
				align-items: center;
				justify-content: space-between;
			}
			.h1{
				.name{
					font-size: 32upx;
					color: #333333;
				}
				.price{
					font-size: 28upx;
					color: #333333;
					font-weight: 600;
					&:before{
						content: "￥";
						font-size: 24upx;
						font-weight: 400;
					}
				}
			}
			.h2{
				margin: 20upx 0 35upx;
				.laber{
					font-size: 22upx;
					color: #555555;
					height: 32upx;
					line-height: 32upx;
					border-radius: 16upx;
					padding: 0 10upx;
					display: block;
					width: 100upx;
					text-overflow: ellipsis;
					white-space: nowrap;
					overflow: hidden;
					text-align: center;
					&.attr-blue{
						color: #2e8ae5;
						background-color: #eaf5ff;	
					}
					&.attr-red{
						color: #ff7f66;	
						background-color: #fdf1ec;	
					}
					&.attr-green{
						color: #0db983;	
						background-color: #e6f8f2;	
					}
				}
				.number{
					font-size: 28upx;
					color: #999;
					&:before{
						content: "*";
						font-size: 24upx;
					}
				}
			}
			.h3{
				.date{
					font-size: 24upx;
					color: #999999;
				}
				.total{
					font-size: 24upx;
					color: #333;
					.price{
						font-size: 28upx;
						color: #333333;
						font-weight: 600;
						&:before{
							content: "￥";
							font-size: 24upx;
							font-weight: 400;
						}
					}
				}
			}
		}
		.foot{
			display: flex;
			justify-content: flex-end;
			padding: 20upx 30upx;
			position: relative;
			.btn{
				font-size: 28upx;
				color: #555555;
				height: 60upx;
				line-height: 60upx;
				width: 160upx;
				text-align: center;
				box-sizing: border-box;
				border: 1px solid #b3b3b3;
				border-radius: 30upx;
				margin-left: 20upx;
				&:first-child{
					margin-left: 0;
				}
				&.attr-blue{
					color: #0db983;
					border-color: #0db983;	
				}
				&.attr-red{
					color: #ff7f66;	
					border-color: #ff7f66;	
				}
			}
			.move{
				width: 33upx;
				height: 7upx;
				position: absolute;
				left: 30upx;
				top: 50%;
				transform: translateY(-50%);
			}
			.movebox{
				position: absolute;
				left: 0;
				top:80upx;
				width:240upx;
				background: #FFFFFF;
				font-size: 24upx;
				color: #333333;
				line-height: 80upx;
				padding: 0 30upx;
				box-sizing: border-box;
				z-index: 10;
				box-shadow: 0 1px 60upx rgba(0,0,0,.2);
				white-space: nowrap;
				border-radius: 4px;
				&:before{
					content: "";
					position: absolute;
					width: 0;
					height: 0;
					left:20upx;
					border-color: transparent;
					border-style: solid;
					top: -18upx;
					border-width: 0 24upx 24upx;
					border-bottom-color: #FFFFFF;
				}
			}
		}
	}


	.modal{
		position: fixed;
		top: 0;
		left: 0;
		z-index: 1050;
		width: 100%;
		height: 100%;
		overflow: hidden;
		background: rgba(0,0,0,.4);
		display: flex;
		align-items: center;
		padding: 0 40upx;
		box-sizing: border-box;
		.modal-dialog{
			position: relative;
			flex: 1;
			background: #FFFFFF;
			border-radius: 15upx;
			.modal-header{
				font-size: 28upx;
				color: #333333;
				text-align: center;
				line-height: 80upx;
				position: relative;
				border-bottom: 1px solid #ebebeb;
				.close{
					width: 23upx;
					height: 23upx;
					position: absolute;
					right: 40upx;
					top: 50%;
					margin-top: -10upx;
				}
			}
			.modal-body{
				padding: 0 30upx;
				box-sizing: border-box;
				.ul{
					display: flex;
					justify-content: flex-start;
					flex-wrap: wrap;
					.li{
						width: 30%;
						text-align: center;
						font-size: 28upx;
						color: #999999;
						height: 78upx;
						line-height: 78upx;
						border: 1px solid #ebebeb;
						border-radius: 10upx;
						box-sizing: border-box;
						margin-right: 5%;
						text-overflow: ellipsis;
						white-space: nowrap;
						overflow: hidden;
						&:nth-child(3n){
							margin-right: 0;
						}
						&:nth-child(n+4){
							margin-top: 20upx;
						}
						&.active{
							color: #0DB983;
							border-color: #0DB983;
							position: relative;
							&:before{
								content: "";
								background: url(../../static/image/icon_checkbox_pre2.png) no-repeat;
								background-size: 100%;
								width: 28upx;
								height: 28upx;
								position: absolute;
								top: 0;
								right: 0;
							}
						}
					}
				}
				.email{
					font-size: 28upx;
					color: #555555;
					border: 1px solid #ebebeb;
					border-radius: 10upx;
					line-height: 98upx;
					height: 98upx;
					margin: 20upx 0;
					padding: 0 30upx;
				}
				.btn{
					height: 84upx;
					line-height: 84upx;
					border-radius: 42upx;
					text-align: center;
					font-size: 32upx;
					width: 100%;
					background:#0db983;
					color: #fff;
				}
				.msg{
					font-size: 28upx;
					color: #999;
					margin: 30upx 0;
					text-align: center;
				}
			}
		}
	
	}
	.share{
		padding: 0;
		.modal-dialog{
			position: absolute;
			bottom: 0;
			width: 100%;
			border-radius: 0;
			border-top-left-radius: 30upx;
			border-top-right-radius: 30upx;
			.sharelist{
				padding: 48upx 0;
				.item{
					display: flex;
					align-items: center;
					margin-bottom: 30upx;
					&:last-child{margin-bottom: 0;}
					.left{
						display: flex;
						align-items: center;
						font-size: 28upx;
						image{
							width: 40upx;height: 40upx;margin-right: 20upx;
						}
						.lb{
							color: #999999;
							margin-left: 10upx;
						}
					}
					.right{
						flex: 1;
						text-align: right;
						image{
							width: 32upx;height: 32upx;
						}
					}
				}
			}
		}
	}
	
	.balance{
		padding-bottom: 100upx !important;
		.price{
			font-size: 60upx;
			text-align: center;
			padding: 60upx 0;
			text{
				&:before{
					content: "￥";
					font-size: 28upx;
				}
			}
		}
		.sharelist{
			padding: 0;
			.right{
				text-align: left !important;
				font-size: 28upx;
				color: #999999;
			}
		}
		.btn{
			height: 85upx;
			line-height: 85upx;
			background: #0DB983;
			font-size: 28upx;
			color: #FFFFFF;
			border-radius: 42.5upx;
			text-align: center;
			margin-top: 30upx;
		}
	}
	.balancepassword{
		padding: 100upx 0 !important;
		.msg{
			color: #2e8ae5 !important;
		}
	}
</style>
