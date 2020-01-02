<template>
	<view class="content">
		<image src="../../static/image/img_phone.png" mode="" class="bgImg"></image>
		<view class="msg">
			绑定的手机号：15212345678
		</view>
		<view class="btn" @click="navTo('/pages/userinfo/Verifyphone')">
			更换手机号
		</view>
	</view>
</template>

<script>
	export default {
		data(){
			return {
				
			}
		},
		methods:{
			navTo(url){
				uni.navigateTo({  
					url
				})  
			},
		}
	}
</script>

<style lang="less">
	page{
		background: #f7f8fa;
	}
	.content{
		padding-top: 210upx;
		.bgImg{
			width: 145upx;
			height: 180upx;
			display: block;
			margin: 0 auto;
		}
		.msg{
			font-size: 32upx;
			color: #000;
			text-align: center;
			margin: 35upx 0 60upx;
		}
		.btn {
		  background-color: rgb(13, 185, 131);
		  height: 84upx;
		  margin: 0 90upx;
		  text-align: center;
		  color: #fff;
		  line-height: 84upx;
		  border-radius: 42upx;
		  font-size: 32upx;
		}

	}
	
</style>
