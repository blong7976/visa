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
				<view class="item" @click="changetype('0')">
					<image src="../../static/image/icon_wechatpay.png" mode="" class="icon"></image>
					微信支付
					<image :src="playType==0?'../../static/image/icon_radio_press.png':'../../static/image/icon_radio.png'" mode="" class="radio"></image>
				</view>
				<view class="item"  @click="changetype('1')">
					<image src="../../static/image/icon_alipay.png" mode="" class="icon"></image>
					支付宝支付
					<image :src="playType==1?'../../static/image/icon_radio_press.png':'../../static/image/icon_radio.png'" mode="" class="radio"></image>
				</view>
			</view>
		</view>
		<view class="btn">
			确认提现
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				playType:0
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
				.icon{
					width: 40upx;
					height: 40upx;
					margin-right: 15upx;
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
	}
</style>
