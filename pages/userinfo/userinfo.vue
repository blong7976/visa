<template>
	<view class="userinfo-box">
		<view class="list-cell b-b">
			<view>头像</view>
			<image src="../../static/image/user.png" class="avatar"></image>
		</view>
		<view class="list-cell b-b">
			<view>昵称</view>
			<view class="content">
				<input type="text" value="" placeholder="请输入昵称" />
			</view>
		</view>
		<view class="list-cell move">
			<view>性别</view>
			<view class="content">
			<picker @change="bindPickerSexChange" :value="index" :range="sex">
				<view class="uni-input">{{sex[index]}}</view>
			</picker>
			</view>
		</view>
		<view class="list-cell mt20 b-b move" >
			<view>绑定手机号</view>
			<view class="content" @click="navTo('/pages/userinfo/setphone')">
				15102988385
			</view>
		</view>
		<view class="list-cell move">
			<view>推荐二维码</view>
			<view class="content">
				<image src="../../static/image/icon_qrcode_s.png" mode="" class="ewm"></image>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data(){
			return{
				sex:['男','女'],
				index: 0,
			}
		},
		methods:{
			navTo(url){
				uni.navigateTo({  
					url
				})  
			}, 
			bindPickerSexChange(e){
				this.index = e.target.value
			}
		}
	}
</script>

<style lang="less">
	page{
		background: #f7f8fa;
	}
	.userinfo-box {
		padding-bottom: 20rpx;
		color: #333;
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
		.avatar {
			width: 100rpx;
			height: 100rpx;
			display: block;
			border-radius: 50%;
		}
		.content {
			font-size: 28rpx;
			color: #666;
			line-height: 1;
			text-align: right;
			.ewm{
				width: 32upx;
				height: 32upx;
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
		right: 30rpx;
	}
</style>
