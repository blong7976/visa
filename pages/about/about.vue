<template>
	<view class="container">
		<view class="logo"></view>
		<view class="name">轻游记</view>
		<view class="version">
			<text>Version1.0.1</text>
			<text>当前是最新版本</text>
		</view>
		<view class="describe">
			轻游记是中国领先的自由行服务平台，是8000万自由行旅行者口碑相传的选择，覆盖60000个国外目的地的攻略，并且提供签证办理的服务。轻游记，一个直链当地的旅游平台
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		methods:{
			
		}
	}
</script>

<style lang='less'>
	page{
		background: #f7f8fa;
		padding-top: 60upx;
		.name{
			text-align: center;
			font-size: 48upx;
			color: #333;
		}
		.version{
			margin-top: 20upx;
			margin-bottom: 40upx;
			text-align: center;
			font-size: 24upx;
			color: #999;
			text{
				display: block;
			}
		}
		.describe{
			font-size: 28upx;
			color: #555;
			margin: 0 60upx;
			line-height: 44upx;
			text-indent: 40upx;
		}
	}
	.logo{
		border-radius: 40upx;
		background-color: rgb(13, 185, 131);
		width: 200upx;
		height: 200upx;
		margin: 0 auto 40upx;
	}
</style>
