<template>
	<view class="content">
		<view class="alert">
			<image src="../../static/image/icon_horn.png" mode="aspectFill" class="icon"></image>
			更换手机号后，下次登录可使用新手机号登录。当前手机号：152 1234 5678
		</view>
		<view class="list-cell b-b mt20">
			<view>手机号</view>
			<view class="content">
				<input type="text" v-model="phoneData.mobile" placeholder="你本人的手机号" @blur="vfphone"/>
			</view>
		</view>
		<view class="list-cell ">
			<view>验证码</view>
			<view class="content">
				<input type="text" v-model="phoneData.code" placeholder="输入短信验证码" />
				<text :class="isConfirm?'getCode send':'getCode'">获取验证码</text>
			</view>
		</view>
		<view class="btn">
			确定
		</view>
	</view>
</template>

<script>
	export default {
		data(){
			return{
				phoneData: {
					mobile: '',
					code:''
				},
				isConfirm:false
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
			}
		}
	}
</script>

<style lang="less">
	page{
		background: #f7f8fa;
	}
	.alert{
		background: #fff;
		padding: 20upx 30upx;
		font-size: 24upx;
		color: #999;
		line-height: 1.5;
		.icon{
			width: 28upx;
			height: 26upx;
			margin-right: 10upx;
			vertical-align: middle;
		}
	}
	.list-cell{
		position: relative;
		width: 100%;
		box-sizing: border-box;
		overflow: hidden;
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: 15px;
		font-size: 28upx;
		color: #333;
		background: #FFFFFF;
		.content {
			font-size: 28rpx;
			color: #666;
			line-height: 1;
			flex: 1;
			margin-left: 30upx;
			display: flex;
			align-items: center;
			justify-content: space-between;
			.getCode{
				font-size: 24upx;
				color: #999;
				padding: 15upx;
				border: 1px solid #999999;
				border-radius: 60upx;
				&.send{
					color: #333333;
					border-color: #333333;
				}
			}
		}
	}
	.mt20{
		margin-top: 20upx;
	}
	.b-b:before{
		content: "";
		height: 1px;
		left: 30upx;
		right: 30upx;
		position: absolute;
		bottom: 0;
		background: #ebebeb;
	}
	.btn {
	  background-color: rgb(13, 185, 131);
	  height: 84upx;
	  margin: 0 90upx;
	  margin-top: 60upx;
	  text-align: center;
	  color: #fff;
	  line-height: 84upx;
	  border-radius: 42upx;
	  font-size: 32upx;
	}
</style>
