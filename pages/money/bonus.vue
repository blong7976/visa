<template>
	<view class="content">
		<image src="../../static/image/bonusBGimg.png" mode="scaleToFill" class="bgImg"></image>
		<view class="cn">
			<image src="../../static/image/img_coin.png" mode="aspectFit" class="icon"></image>
			<view class="title">
				奖励金
			</view>
			<view class="info">
				<view class="smTitle">奖励金余额</view>
				<view class="price">
					158,00
				</view>
				<view class="btn color" @click="navTo('/pages/money/Into_account')">
					转入账户
				</view>
				<view class="btn" @click="navTo('/pages/money/withdrawal')">
					提现
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				
			}
		},
		methods:{
			navTo(url){
				uni.navigateTo({  
					url
				})  
			}
		}
	}
</script>

<style lang="less">
	.bgImg{
		width: 100%;
		top: 0;
		height: 100%;
		bottom: 0;
		position: fixed;
	}
	.cn{
		position: absolute;
		width: 100%;
		z-index: 10;
	}
	.icon{
		width: 70upx;
		height: 74upx;
		margin: 0 auto;
		display: block;
	}
	.title{
		font-size: 28upx;
		color: #fff;
		text-align: center;
		margin: 15upx 0 38upx;
	}
	.info{
		background: #FFFFFF;
		padding: 90upx 100upx;
		margin: 0 30upx;
		border-radius: 15upx;
		.smTitle{
			font-size: 24upx;
			text-align: center;
			color: #333333;
		}
		.price{
			font-size: 50upx;
			text-align: center;
			color: #000;
			margin-top: 30upx;
			font-weight: bold;
			&:before{
				content: "￥";
				font-size: 28upx;
				font-weight: 400;
			}
		}
		.btn{
			height: 84upx;
			width: 100%;
			line-height: 84upx;
			border-radius: 42upx;
			text-align: center;
			font-size: 32upx;
			background: #ebebeb;
			color: #0fb87f;
			margin-bottom: 30upx;
		}
		.color{
			background:#0fb87f;
			color: #fff;
			margin-top: 115upx;
		}
	}
</style>
