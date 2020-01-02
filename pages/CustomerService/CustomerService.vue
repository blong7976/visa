<template>
	<view class="content">
		<view class="erect">
			沟通改变世界
		</view>
		<view class="Messagebtn">
			<view class="child">
				<image src="../../static/image/icon_chat.png" mode="" class="icon"></image>
				<view class="laber">聊天</view>
			</view>
			<view class="child">
				<image src="../../static/image/icon_phone.png" mode=""  class="icon"></image>
				<view class="laber">电话</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: '客服s'
			}
		},
		onLoad() {

		},
		methods: {

		}
	}
</script>

<style lang="less">
	.content{
		background-color: #FFFFFF;
	}
	.erect {
		writing-mode: vertical-rl;
		color: #999999;
		font-size: 40upx;
		width: 50upx;
		margin: 0 auto;
		letter-spacing: 11px;
		padding: 200upx 0;
	}
	.Messagebtn{
		width: 100%;
		display: flex;
		justify-content: space-between;
		.child{
			flex: 1;
			align-items: center;
			text-align: center;
			.icon{
				width: 152upx;
				height: 152upx;
			}
			.laber{
				font-size: 28upx;
				color: #999999;
			}
		}
	}
</style>
