<template>
	<view class="content">
		<view class="list-cell b-b">
			<view>原密码</view>
			<view class="content">
				<input type="password" placeholder="输入原密码"/>
			</view>
		</view>
		<view class="list-cell b-b ">
			<view>新密码</view>
			<view class="content">
				<input type="password" placeholder="填写新密码"/>
			</view>
		</view>
		<view class="list-cell ">
			<view>确认密码</view>
			<view class="content">
				<input type="password"  placeholder="再次输入密码"/>
			</view>
		</view>
		<view class="msg">
			密码必须是8-16位的数字、字符组合（不能是纯数字）
			<text>忘记原密码</text>
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
		
		}
	}
</script>

<style lang="less">
	page{
		background: #f7f8fa;
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
	  margin: 0 30upx;
	  margin-top: 60upx;
	  text-align: center;
	  color: #fff;
	  line-height: 84upx;
	  border-radius: 42upx;
	  font-size: 32upx;
	}
	.msg{
		font-size: 28upx;
		color: #999;
		margin:20upx 30upx;
		text{
			display: block;
			color: #60a6ea;
			margin-top: 10upx;
			cursor: pointer;
		}
	}
</style>
