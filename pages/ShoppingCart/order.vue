<template>
	<view class="content">
		<view class="_head">
			<image src="../../static/image/moneybg.png" mode="" class="pgimg"></image>
			<block v-if="orderState==1">
				<view class="title">
					等待买家付款
				</view>
			</block>
			<block v-if="orderState==2">
				<view class="title success">
					交易成功
				</view>
			</block>
			<block v-if="orderState==3">
				<view class="title success">
					退款成功
				</view>
			</block>
			<block v-if="orderState==4">
				<view class="title cancel">
					已取消
				</view>
			</block>
		</view>
		<view class="_body">
			<view class="address">
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
			
			<view class="orderinfo">
				<view class="h1">
					<text class="name">日本一个月单次旅游签证</text>
					<text class="price">100</text>
				</view>
				<view class="h2">
					<text class="laber attr-blue">电子签</text>
					<text class="number">1</text>
				</view>
				<view class="total">
					<view class="h3">
						<text>商品合计</text>
						<text>￥600</text>
					</view>
					<view class="h3">
						<text>实付款</text>
						<text class="price">￥588.50</text>
					</view>
				</view>
			</view>
			
			<view class="section">
				<view class="head">
					订单信息
				</view>
				<view class="li">
					<view class="left">
						<text>订单编号</text><text>201902605</text>
					</view>
					<view class="right">
						<text class="copy">复制</text>
					</view>
				</view>
				<view class="li">
					<view class="left">
						<text>订单编号</text><text>201902605</text>
					</view>
				</view>
			</view>
			
		</view>
		
		
		<view class="tui-tabbar">
			<view class="tui-flex-end" v-if="orderState==2">
				<image src="../../static/image/icon_tpot.png" mode="aspectFit" class="move" @click="handleMove"></image>
				<view class="movebox" v-if="move">
					<view @click="move=false">删除订单</view>
				</view>
			</view>
			<view class="btn-group">
				<block v-if="orderState==1">
					<view class="btn" >
						取消订单
					</view>
					<view class="btn play" >
						付款
					</view>
				</block>
				<block v-if="orderState==2">
					<view class="btn" >
						评价
					</view>
					<view class="btn" >
						申请开票
					</view>
					<view class="btn zcplay" >
						再次购买
					</view>
				</block>
				<block v-if="orderState==4 || orderState==3">
					<view class="btn" >
						删除订单
					</view>
					<view class="btn zcplay" >
						再次购买
					</view>
				</block>
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				orderState:null,
				move:false,
				/**
				 * 订单状态 orderState  
				 * 0：待提交资料 
				 * 1：待付款
				 * 2：已完成
				 * 3：退款成功
				 * 4：已取消   
				 * **/
			}
		},
		onLoad(option){
			if(option.type){
				this.orderState = option.type
			}
		},
		methods:{
			handleMove(){
				this.move =! this.move
			}
		}
	}
</script>

<style lang="less">
	page{
		background: #f7f8fa;padding-bottom: 120upx;
	}
	._head{
		position: relative;
		width: 100%;
		height: 247upx;
		.pgimg{
			width: 100%;
			height: 100%;
			position: absolute;
			top: 0;
			left: 0;
			right: 0;
		}
		.title{
			position: relative;
			font-size: 40upx;
			color: #FFFFFF;
			z-index: 100;
			text-align: center;
			top: 65upx;
			display: flex;
			align-items: center;
			justify-content: center;
			&:before{
				content: "";
				width: 38upx;
				height: 38upx;
				background: url(../../static/image/icon_time.png) no-repeat;
				background-size: 100%;
				display: block;
				margin-right: 20upx;
			}
			&.cancel:before{
				content: "";
				width: 38upx;
				height: 38upx;
				background: url(../../static/image/icon_cancel.png) no-repeat;
				background-size: 100%;
				display: block;
				margin-right: 20upx;
			}
			&.success:before{
				content: "";
				width: 38upx;
				height: 38upx;
				background: url(../../static/image/icon_complete.png) no-repeat;
				background-size: 100%;
				display: block;
				margin-right: 20upx;
			}
		}
	}
	._body{
		padding:0 30upx;
		margin-top: -60upx;
		position: relative;
		z-index: 101;
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
		.orderinfo{
			background: #FFFFFF;
			margin-top: 20upx;
			box-sizing: border-box;
			padding:40upx 30upx;
			background: #fff;
			position: relative;
			overflow: hidden;
			border-radius: 20upx;
			.h1,.h2{
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
				margin: 20upx 0 30upx;
				position: relative;
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
			.total{
				padding-top: 20upx;
				border-top: 1px solid #ebebeb;
				.h3{
					display: flex;
					justify-content: space-between;
					align-items: center;
					font-size: 24upx;
					color: #333333;
					line-height: 55upx;
					.price{
						font-size: 32upx;
						color: #ff7f66;
					}
				}
			}
		}
		.section{
			padding:30upx;
			background: #fff;
			position: relative;
			overflow: hidden;
			border-radius: 20upx;
			margin-top: 20upx;
			.head{
				font-size: 28upx;color: #333333;margin-bottom: 20upx;
			}
			.li{
				display: flex;
				align-items: center;
				justify-content: space-between;
				font-size: 24upx;
				color: #999999;
				line-height: 50upx;
				.copy{
					color: #0db983;
				}
				.left{
					text:first-child{
						margin-right: 30upx;
					}
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
				left: 30upx;
				bottom:90upx;
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
					bottom: -18upx;
					border-width: 24upx 24upx 0 ;
					border-top-color: #FFFFFF;
				}
			}
		}
		.btn-group{
			display: flex;
			align-items: center;
			justify-content: flex-end;
			flex: 1;
			.btn{
				height: 60upx;
				line-height: 60upx;
				width: 160upx;
				text-align: center;
				border-radius: 36upx;
				font-size: 28upx;
				border: 1px solid #b3b3b3;
				margin-left: 20upx;
				&:first-child{
					margin-left: 0;
				}
				&.play{
					color: #FFFFFF;
					background: #ff7f66;
					border-color:#ff7f66;
				}
				&.zcplay{
					color: #0DB983;
					border-color:#0DB983;
				}
			}
		}
	
	}
</style>
