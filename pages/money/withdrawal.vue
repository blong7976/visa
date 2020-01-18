<template>
	<view class="content">
		<view class="info">
			<view class="title">
				提现金额
			</view>
			<view class="input">
				<input type="number" maxlength="15"/>
			</view>
		</view>
		<view class="info">
			<view class="title">
				提现到
			</view>
			<view class="select">
				<block v-if="hasBankcard">
					<view class="item" @click="changetype('0')">
						<image src="../../static/image/icon_jianshe.png" mode="" class="icon"></image>
						建设银行（0780）
						<image :src="playType==0?'../../static/image/icon_radio_press.png':'../../static/image/icon_radio.png'" mode="" class="radio"></image>
					</view>
					<view class="item"  @click="changetype('1')">
						<image src="../../static/image/icon_nongye.png" mode="" class="icon"></image>
						农业银行
						<image :src="playType==1?'../../static/image/icon_radio_press.png':'../../static/image/icon_radio.png'" mode="" class="radio"></image>
					</view>
					<view class="item"  @click="changetype('2')">
						<!-- <image src="../../static/image/icon_alipay.png" mode="" class="icon"></image> -->
						使用新卡提现
						<image :src="playType==2?'../../static/image/icon_radio_press.png':'../../static/image/icon_radio.png'" mode="" class="radio"></image>
					</view>
				</block>
				<block v-else>
					<view class="item addbankcard move"  @click="navTo('/pages/money/BankcardCode')">
						添加银行卡
					</view>
				</block>
			</view>
		</view>
		<view :class="hasBankcard?'btn':'btn disabled'" @click="submitOrder">
			确认提现
		</view>
		
		<!--  提现到 -> 支付密码 -->
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
	import wakaryInput from '@/components/wakary-input/wakary-input.vue'
	export default{
		components:{
			wakaryInput
		},
		data(){
			return{
				playType:0,
				balancePSDModalShow:false,
				// 状态：没有支付密码
				userInfo:{
					payPassword:null
				},
				// 是否已绑定银行卡 false 的时候 显示绑定银行卡 否则显示已绑定卡供选择 
				hasBankcard:false
			}
		},
		methods:{
			navTo(url){
				uni.navigateTo({  
					url
				})  
			},
			changetype(type){
				this.playType = type
			},
			submitOrder(){
				// 用户未绑定银行卡 
				if(!this.hasBankcard){return}
				// 有支付密码的时候，跳转
				// 提交成功页面： this.navTo('/pages/money/wdSuccess')
				if(this.userInfo.payPassword){
					this.balancePSDModalShow = true
				}else{
					this.navTo('/pages/money/nopaypd')
				}
			}
			
		}
	}
</script>

<style lang="less">
	page {
		background-color: #f7f8fa;
		padding-top: 20upx;
	}
	.info{
		margin:0 30upx;
		background: #FFFFFF;
		border-radius: 15upx;
		margin-bottom: 20upx;
		.title{
			line-height: 90upx;
			height: 90upx;
			font-size: 32upx;
			padding:0 30upx;
			border-bottom: 1px solid #ebebeb;
		}
		.input{
			padding: 0 30upx;
			display: flex;
			height: 128upx;
			line-height: 128upx;
			position: relative;
			&:before{
				content: "￥";
				font-size: 30upx;
				position: relative;
				top: 10upx;
				margin-right: 10upx;
			}
			input{
				font-size: 64upx;
				color: #333333;
				height: 128upx;
				line-height: 128upx;
			}
		}
		.select{
			padding: 20upx 30upx;
			.item{
				line-height: 70upx;
				height: 70upx;
				font-size: 28upx;
				display: flex;
				align-items: center;
				position: relative;
				padding-left: 52upx;
				.icon{
					width: 40upx;
					height: 40upx;
					margin-right: 15upx;
					position: absolute;
					left: 0;
				}
				.radio{
					width: 32upx;
					height: 32upx;
					position: absolute;
					right: 0;
					top: 50%;
					margin-top: -16upx;
				}
			}
			.addbankcard{
				padding-left: 0;
			}
			.move{padding-right: 60upx;}
			.move:after{
				content: " ";
				height: 11px;
				width: 11px;
				border-width: 2px 2px 0 0;
				border-color: #b3b3b3;
				border-style: solid;
				-webkit-transform: matrix(0.5, 0.5, -0.5, 0.5, 0, 0);
				transform: matrix(0.5, 0.5, -0.5, 0.5, 0, 0);
				position: absolute;
				top: 50%;
				margin-top: -7px;
				right: 0;
			}
		}
	}
	.btn{
		height: 84upx;
		line-height: 84upx;
		border-radius: 42upx;
		text-align: center;
		font-size: 32upx;
		background:#0fb87f;
		color: #fff;
		margin: 60upx 40upx 0;
		&.disabled{
			background: #ebebeb;
			color: #999999;
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
