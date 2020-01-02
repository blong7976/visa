<template>
	<view class="content">
		<view class="info">
			<view class="title">
				转入账户金额
			</view>
			<view class="input">
				<input type="number" maxlength="15"/>
			</view>
		</view>
		<view class="btn">
			转入
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
	page {
		background-color: #f7f8fa;
		padding-top: 20upx;
	}
	.info{
		margin:0 30upx;
		background: #FFFFFF;
		border-radius: 15upx;
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
