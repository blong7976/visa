<template>
	<view class="app">
		<view class="user-section">
			<image src="../../static/image/moneybg.png" mode="" class="bg"></image>
			<view class="info">
				<view class="p1">
					账户余额  
					<!-- #ifdef MP -->
					<text class="chlist" @click="navTo('/pages/money/moneylist')">交易记录></text>
					<!-- #endif -->
				</view>
				<view class="price">
					154,89
				</view>
			</view>
		</view>
		<view class="cover-container">
			<view class="tj-sction">
				<view class="item">
					<view class="title" >
						<text @click="navTo('/pages/money/bonus')">奖励金</text> > 
						<image src="../../static/image/icon_help.png" mode="aspectFit" @click="newVersion=true"></image>
					</view>
					<view class="content">
						115,85
					</view>
				</view>
				<view class="item">
					<view class="title">
						积分
					</view>
					<view class="content">
						2850
					</view>
				</view>
			</view>
			<view class="navs">
				<view class="list-cell" @click="navTo('/pages/money/recharge')">
					<text class="cell-tit">充值</text>
					<text class="cell-more yticon icon-you"></text>
				</view>
				<view class="list-cell" @click="navTo('/pages/money/banklist')">
					<text class="cell-tit">银行卡</text>
					<text class="cell-more yticon icon-you"></text>
				</view>
				<view class="list-cell m-t"  @click="navTo('/pages/money/writeCode')">
					<text class="cell-tit">支付密码</text>
					<text class="cell-tip">未设置</text>
					<text class="cell-more yticon icon-you"></text>
				</view>
			</view>
		</view>
		<!-- 代理，奖励金 -->
		<view class="modal" v-if="newVersion">
			<view class="modal-body">
				<image src="../../static/image/jiangjinbg.png" mode=""></image>
				<view class="content">
					<text class="msg">成为代理商，获取奖励金 详情请联系客服</text>
				</view>
				<view class="btn">
					联系客服
				</view>
				<view class="close" @click="closeModal">
					<image src="../../static/image/icon_close_w.png" mode=""></image>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				newVersion:false
			}
		},
		methods:{
			navTo(url){
				uni.navigateTo({  
					url
				})  
			}, 
			closeModal(){
				this.newVersion = false
			},
			// #ifndef MP
			onNavigationBarButtonTap(e) {
				console.log(e)
				const index = e.index;
				if (index === 0) {
					this.navTo('/pages/money/moneylist');
				}
			},
			// #endif
		}
	}
</script>

<style lang="less">
	page {
		background-color: #f7f8fa;
	}
	.user-section{
		height: 314upx;
		padding: 0 40upx;
		position: relative;
		.bg{
			position: absolute;
			left: 0;
			top: 0;
			width: 100%;
			height: 100%;
		}
		.info{
			position: relative;
			z-index: 1;
			padding-top: 38upx;
			.p1{
				font-size: 28upx;
				color: #fff;
				.chlist{
					float: right;
				}
			}
			.price{
				font-size: 50upx;
				color: #fff;
				font-weight: bold;
				margin-top: 30upx;
				&:before{
					content: "￥";
					font-size: 28upx;
					font-weight: 400;
					margin-right: 6upx;
				}
			}
		}
	}
	.cover-container{
		padding: 0 30upx;
		margin-top: -100upx;
		position: relative;
		z-index: 10;
		.tj-sction{
			padding: 45upx 0;
			border-radius: 15upx;
			height: 75upx;
			background: #FFFFFF;
			display: flex;
			justify-content: space-between;
			.item{
				flex: 1;
				text-align: center;
				position: relative;
				.title{
					font-size: 24upx;
					color: #999999;
					display: flex;
					align-items: center;
					justify-content: center;
					image{
						width: 22upx;
						height: 22upx;
						margin-left: 10upx;
					}
				}
				.content{
					font-size: 32upx;
					color: #333;
					font-weight: bold;
					margin-top: 4upx;
				}
				&:first-child:before{
					content: "";
					width: 1px;
					height: 100%;
					background: #ebebeb;
					position: absolute;
					right: 0;
					top: 0;
				}
				&:first-child .content:before{
					content: "￥";
					font-size: 24upx;
					font-weight: 400;
				}
			}
			
		}
	}
	
	.navs{
		border-radius: 15upx;
		background: #FFFFFF;
		margin-top: 20upx;
		.list-cell{
			display:flex;
			align-items:baseline;
			padding: 20upx 30upx;
			line-height:60upx;
			position:relative;
			background: #fff;
			justify-content: center;
			&.log-out-btn{
				margin: 40upx 30upx;
				border: 1px solid #ff7f66;
				border-radius: 50upx;
				padding: 0;
				line-height: 84upx;
				background: #f7f8fa;
				.cell-tit{
					color: #ff7f66;
					font-size: 32upx;
					text-align: center;
				}
			}
			&.cell-hover{
				background:#fafafa;
			}
			&.b-b:after{
				left: 30upx;
				content: "";
				height: 1px;
				right: 30upx;
				background: #ebebeb;
				position: absolute;
				bottom: 0;
			}
			.cell-more{
				align-self: baseline;
				font-size:28upx;
				color:#666;
				margin-left:10upx;
			}
			.cell-tit{
				flex: 1;
				font-size: 28upx;
				color: #333;
				margin-right:10upx;
			}
			.cell-tip{
				font-size: 28upx;
				color: #b3b3b3;
			}
		}
	}
	
	.modal{
		position: fixed;
		top:0;
		left:0;
		bottom:0;
		right: 0;
		background: rgba(0,0,0,.5);
		z-index: 999;
		.modal-body{
			position: fixed;
			left: 50%;
			top: 50%;
			margin: auto;
			background: #fff;
			z-index: 9999;
			transition: all 0.3s ease-in-out;
			box-sizing: border-box;
			transform: translate(-50%, -50%) scale(1);
			width: 560upx;
			padding-bottom: 50upx;
			border-radius: 10px;
			image{
				width: 100%;
				height: 242upx;
				border-top-left-radius: 10px;
				border-top-right-radius: 10px;
			}
			.Version{
				position: absolute;
				top: 130upx;
				left:50%;
				transform: translateX(-50%);
				font-size: 28upx;
				color: #fff;
				background-color: #ffc44c;
				text-align: center;
				height: 40upx;
				padding:0 20upx;
				display: flex;
				align-items: center;
				justify-content: center;
				border-radius: 20upx;
			}
			.close{
				width: 30upx;
				height: 30upx;
				position: absolute;
				bottom: -70upx;
				left: 50%;
				transform: translateX(-50%);
				image{
					width: 100%;height: 100%;
				}
			}
			.content{
				width: 100%;
				padding: 30upx 100upx;
				box-sizing: border-box;
				text{
					display: block;
				}
				.msg{
					font-size: 28upx;
					color: #333;
					line-height: 1.5;
					margin-bottom: 15upx;
					text-align: center;
				}
			}
			.btn {
			  background-color: #0db983;
			  width: 380upx;
			  height: 72upx;
			  text-align: center;
			  line-height: 72upx;
			  border-radius: 36upx;
			  margin: 0 auto;
			  margin-top: 0upx;
			  color: #FFFFFF;
			  font-size: 32upx;
			  box-shadow: 0 1px 22px 0 rgb(180, 220, 208), 0 4px 8px 0 rgb(237, 241, 240);
			}
			.nobg{
				background: transparent;
				color:#999;
				font-size: 28upx;
				margin-top: 4px;
				box-shadow: none;
			}
		}
	}
</style>
