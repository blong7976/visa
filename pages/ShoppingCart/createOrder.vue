<template>
	<view class="content">
		<view class="address" @click="navTo('/pages/address/address')">
			<view class="list b-b">
				<view class="wrapper">
					<view class="u-box">
						<image src="../../static/image/icon_location_big.png" mode="aspectFit"></image>
						<text class="name">刘蓓山</text>
						<text class="mobile">17612345678</text>
					</view>
					<view class="address-box">
						<text class="address">广东省深圳市福田区皇岗街道办事处皇岗商务中心55楼滴加有限公司</text>
					</view>
				</view>
				<text class="yticon icon-you"></text>
				<image src="../../static/image/border-back.png" mode="aspectFit" class="border-img"></image>
			</view>
		</view>
		
		<view class="playType">
			<text>支付方式</text>
			<view class="right" @click="dblplayTypeModalShow">
				<block v-if="playType==0">
					<image src="../../static/image/icon_balance.png" mode="aspectFit"></image>余额支付
				</block>
				<block v-if="playType==1">
					<image src="../../static/image/icon_wechatpay.png" mode="aspectFit"></image>微信支付
				</block>
				<block v-if="playType==2">
					<image src="../../static/image/icon_alipay.png" mode="aspectFit"></image>支付宝支付
				</block>
				<text class="yticon icon-you"></text>
			</view>
		</view>
		
		<view class="orderinfo">
			<view class="title">
				越南三个月多次商务签证
			</view>
			<text class="attr attr-blue">电子签</text>
			<view class="flex-box">
				<view class="price">
					<text class="value">
						<text class="em">¥</text>200
					</text>/人
				</view>
				<uni-number-box
					class="step"
					:min="1" 
					:value="info.number"
					:isMin="info.number===1"
					:disabled="true"
					@eventChange="numberChange"
				></uni-number-box>
			</view>
			<view class="remark">
				<text>订单备注</text>
				<input type="text" value="" placeholder="选填"/>
			</view>
		</view>
		
		<view class="deduction">
			<view class="list" @click="info.deduction=0">
				<view class="left">
					<image v-if="info.deduction==0" src="../../static/image/icon_checkbox_pre.png" mode="aspectFit"></image>
					<image v-else src="../../static/image/icon_checkbox.png" mode="aspectFit"></image>积分抵扣
				</view>
				<view class="right">
					无可用
				</view>
			</view>
			<view class="list" @click="info.deduction=1">
				<view class="left">
					<image v-if="info.deduction==1" src="../../static/image/icon_checkbox_pre.png" mode="aspectFit"></image>
					<image v-else src="../../static/image/icon_checkbox.png" mode="aspectFit"></image>奖励金抵扣
				</view>
				<view class="right">
					最高可抵￥12.50
				</view>
			</view>
		</view>
		
		<view class="totalbox">
			<view class="li">
				订单金额 <text>￥200</text>
			</view>
			<view class="li">
				积分抵扣 <text class="red">-￥0.00</text>
			</view>
			<view class="li">
				奖励金抵扣 <text class="red">-￥12.50</text>
			</view>
		</view>
		
		<view class="tui-tabbar">
			<view class="tui-flex-end">
				合计<text>187.88</text>
			</view>
			<!-- @click="navTo('/pages/ShoppingCart/orderDetaile')" -->
			<view class="btn" @click="submitOrder">
				提交订单
			</view>
		</view>
		
		
		<!-- 支付方式 -->
		<!-- <view class="modal share" v-if="playTypeModalShow">
			<view class="modal-dialog ">
				<view class="modal-content">
					<view class="modal-header">
						支付方式
						<image src="../../static/image/icon_close.png" mode="aspectFit" class="close" @click="playTypeModalShow = false"></image>
					</view>
					<view class="modal-body">
						<view class="sharelist">
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
		</view> -->
		
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
	import uniNumberBox from '@/components/uni-number-box.vue'
	import wakaryInput from '@/components/wakary-input/wakary-input.vue'
	export default{
		components:{
			uniNumberBox,wakaryInput
		},
		data(){
			return{
				info:{
					number:1,
					deduction:0
				},
				currenttap:true,
				playTypeModalShow:false,
				playType:0,
				balanceModalShow:false,
				balancePSDModalShow:false
			}
		},
		methods:{
			navTo(url){
				uni.navigateTo({
					url
				})
			},
			numberChange(e){
				this.info.number = e
			},
			dblplayTypeModalShow(){
				this.currenttap = false
				this.playTypeModalShow = true
			},
			selectplayType(e){
				this.playType = e
				if(this.currenttap){
					this.playTypeModalShow = false
					this.balanceModalShow = true
				}else{
					this.playTypeModalShow = false
				}
			},
			handleSelectplayType(){
				this.playTypeModalShow = true
				this.balanceModalShow = false
			},	
			balancePlay(){
				this.balanceModalShow = false
				this.balancePSDModalShow = true
			},
			submitOrder(){
				this.currenttap = true
				this.playTypeModalShow = true
			}
		}
	}
</script>

<style lang="less" >
	page{
		background-color: #f7f8fa;
	}
	.content{
		padding: 20upx 30upx 120upx;
		.address{
			position: relative;
			.list{
				display: flex;
				align-items: center;
				padding:40upx 30upx;
				background: #fff;
				position: relative;
				overflow: hidden;
				border-radius: 10upx;
				.border-img{
					position: absolute;
					left: 0;
					bottom: 0;
					display: block;
					width: 100%;
					height: 2px;
					/deep/div{
						background-size: 100% !important;
					}
				}
				&:before{
					content: "";
					position: absolute;
					left: 30upx;
					right: 30upx;
					bottom: 0;
					background: #ebebeb;
					height: 1px;
				}
				.u-box{
					font-size: 32upx;
					color: #333;
					display: flex;
					align-items: center;
					image{
						width: 26upx;
						height: 32upx;
					}
					.name{
						margin-right: 30upx;
						margin-left: 20upx;
					}
					.tag{
						font-size: 22upx;
						color: #fff;
						background: #ff7f66;
						margin-left: 10upx;
						border-radius: 30upx;
						padding: 4upx 10upx;
						line-height: 1;
					}
				}
				.address-box{
					display: flex;
					align-items: center;
					margin-top: 16upx;
					.address{
						font-size: 24upx;
						color: #555;
					}
				}
				.yticon{
					display: flex;
					align-items: center;
					height: 80upx;
					font-size: 40upx;
					color: #333;
					padding-left: 60upx;
				}
			}
			.list:last-of-type:before{
				display: none;
			}
		}
		.playType{
			display: flex;
			align-items: center;
			justify-content: space-between;
			padding: 40upx 30upx;
			background: #FFFFFF;
			margin-top: 20upx;
			font-size: 28upx;
			color: #333333;
			border-radius: 10upx;
			.right{
				display: flex;
				align-items: center;
				line-height: 40upx;
				position: relative;
				image{
					width: 40upx;
					height: 40upx;
					margin-right: 20upx;
				}
				.yticon{
					margin-left: 20upx;
				}
			}
		}
		.orderinfo{
			padding: 40upx 30upx;
			background: #FFFFFF;
			border-radius: 10upx;
			margin-top: 20upx;
			display:flex;
			flex-direction: column;
			flex: 1;
			overflow: hidden;
			position:relative;
			.title,.price{
				font-size:28upx;
				color: #555555;
				height: 40upx;
				line-height: 40upx;
			}
			.title{
				text-overflow: ellipsis;
				white-space: nowrap;
				overflow: hidden;
				font-size: 32upx;
				color: #333333;
				font-weight: bold;
			}
			.attr{
				font-size: 22upx;
				color: #555555;
				height: 32upx;
				line-height: 32upx;
				border-radius: 16upx;
				padding: 0 10upx;
				display: block;
				margin: 20upx 0;
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
			}
			.flex-box{
				display: flex;
				align-items: center;
				justify-content: space-between;
				margin-bottom: 20upx;
			}
			.price{
				height: 50upx;
				line-height:50upx;
				font-size: 24upx;
				color: #999999;
				.value{
					font-size: 32upx;
					color: #ff7f66;
					.em{
						font-size: 22upx;
					}
				}
			}
			.step{
				position: relative;
			}
			.remark{
				display: flex;
				align-items: center;
				justify-content: space-between;
				font-size: 28upx;
				color: #333333;
				padding-top: 20upx;
				border-top: 1px solid #ebebeb;
				input{
					text-align: right;
				}
			}
		}
		.deduction{
			background: #FFFFFF;
			border-radius: 10upx;
			padding: 40upx 30upx;
			margin-top: 20upx;
			.list{
				display: flex;
				align-items: center;
				justify-content: space-between;
				margin-bottom: 40upx;
				&:last-child{
					margin-bottom: 0;
				}
				.left{
					flex: 1;
					font-size: 28upx;
					color: #333333;
					display: flex;
					align-items: center;
					image{
						width: 32upx;
						height: 32upx;
						margin-right: 20upx;
					}
				}
				.right{
					flex: 1;
					background: #f7f8fa;
					line-height: 50upx;
					font-size: 24upx;
					color: #999999;
					border: 1px solid #ebebeb;
					box-sizing: border-box;
					border-radius: 3px;
					text-indent: 20upx;
				}
			}
		}
		.totalbox{
			background: #FFFFFF;
			padding: 20upx 30upx;
			border-radius: 10upx;
			margin-top: 20upx;
			.li{
				display: flex;
				align-items: center;
				justify-content: space-between;
				font-size: 28upx;
				color: #333333;
				height: 70upx;
				line-height: 70upx;
				.red{
					color: #ff7f66;
				}
			}
		}
	}
	.tui-tabbar{
		background: #FFFFFF;
		height: 100upx;
		display: flex;
		align-items: center;
		justify-content: space-between;
		position: fixed;
		bottom: 0;
		left: 0;
		right: 0;
		box-sizing: border-box;
		padding: 0 30upx;
		.tui-flex-end{
			font-size: 28upx;
			color: #999999;
			text{
				font-size: 34upx;
				color: #ff7f66;
				font-weight: 600;
				&:before{
					content: "￥";
					font-size: 28upx;
					font-weight: 400;
					margin-left: 10upx;
				}
			}
		}
		.btn{
			height: 72upx;
			line-height: 72upx;
			width: 218upx;
			text-align: center;
			border-radius: 36upx;
			font-size: 28upx;
			color: #FFFFFF;
			background: #ff7f66;
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
