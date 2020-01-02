<template>
	<view class="content">
		<view class="title">
			验证码登录
		</view>
		<view class="form">
			<view class="form-group">
				<input type="text" v-model="phoneData.mobile" placeholder="请输入手机号码" @blur="vfphone"/>
				<image src="../../static/image/icon_del_s.png" v-if="phoneData.mobile" mode="aspectFit" class="close" @click="phoneData.mobile = ''"></image>
			</view>
			<view class="form-group">
				<input type="text" v-model="phoneData.code" placeholder="请输入短信验证码"/>
				<text :class="isConfirm?'getCode send':'getCode'">获取验证码</text>
			</view>
			<view :class="isConfirm?'btn login':'btn'">
				登陆
			</view>
			<view class="m-unlogin">
				<text @click="navTo('/pages/login/registered')">注册</text>
				<text @click="navTo('/pages/login/loginpsd')">密码登陆</text>
			</view>
		</view>
		<view class="footer">
			<view class="title">
				<text></text>
				更多登陆方式
				<text></text>
			</view>
			<view class="list">
				<image src="../../static/image/icon_wechat_sign.png" mode="aspectFit"></image>
				<image src="../../static/image/icon_alipay_sign.png" mode="aspectFit"></image>
				<image src="../../static/image/icon_qq_sign.png" mode="aspectFit"></image>
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				phoneData: {
					mobile: '',
					code:''
				},
				isConfirm:false,
			}
		},
		methods:{
			vfphone(e){
				if(!/(^1[3|4|5|7|8][0-9]{9}$)/.test(e.detail.value)){
					uni.showToast({
						icon:'none',
						title:'请输入正确的手机号码'
					})
					this.isConfirm = false
					return;
				}else{
					this.isConfirm = true
				}
			},
			navTo(url){
				uni.navigateTo({
					url
				})
			}
		}
	}
</script>

<style lang="less" scoped>
	.content{
		box-sizing: border-box;
		padding: 60upx 70upx;
	}
	.title{
		font-size: 56upx;
		color: #333333;
	}
	.form{
		margin-top: 80upx;
		.form-group{
			margin-bottom: 20upx;
			display: flex;
			align-items: center;
			justify-content: space-between;
			padding: 18upx 0;
			border-bottom: 1px solid #f2f2f2;
			.getCode{
				font-size: 24upx;
				color: #999999;
				width: 150upx;
				height: 50upx;
				text-align: center;
				line-height: 50upx;
				border: 1px solid #999;
				border-radius: 10upx;
				cursor: pointer;
				&.send{
					color: #333333;
					color: #333333;
				}
			}
			.close{
				width: 30upx;
				height: 30upx;
			}
		}
		.btn{
			font-size: 34upx;
			color: #999999;
			height: 84upx;
			line-height: 84upx;
			border-radius: 42upx;
			background: #ebebeb;
			margin-top:58upx;
			text-align: center;
			&.login{
				background: #0DB983;
				color: #FFFFFF;
			}
		}
		.m-unlogin{
			display: flex;
			justify-content: space-between;
			font-size: 30upx;
			color: #777;
			margin-top: 45upx;
		}
	}
	.footer{
		position: fixed;
		bottom: 0;
		left: 0;
		right: 0;
		z-index: 999;
		box-sizing: border-box;
		padding: 0 130upx;
		text-align: center;
		.title{
			font-size: 28upx;
			color: #999999;
			display: flex;
			align-items: center;
			justify-content: space-between;
			text{
				display: block;
				height: 1px;
				width: 110upx;
				background: #ebebeb;
			}
		}
		.list{
			padding: 30upx 0 110upx;
			display: flex;
			align-items: center;
			justify-content: space-between;
			image{
				width: 80upx;
				height: 80upx;
			}
		}
	}
</style>
