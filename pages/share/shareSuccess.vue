<template>
	<view class="content">
		<image src="../../static/image/img_success.png" mode="aspectFill"></image>
		<view class="msg">
			推荐成功
		</view>
	</view>
</template>

<script>
	export default{
		methods:{
			navTo(url){
				uni.navigateTo({  
					url
				})  
			}, 
			// #ifndef MP
			onNavigationBarButtonTap(e) {
				const index = e.index;
				if (index === 0) {
					this.navTo('/pages/share/detailes');
				}
			},
			// #endif
		}
	}
</script>

<style lang="less" scoped>
	page {
		background-color: #f7f8fa;
		padding-top: 200upx;
	}
	image{
		width: 144upx;
		height: 181upx;
		display: block;
		margin: 0 auto;
	}
	.msg{
		font-size: 32upx;
		color: #333333;
		text-align: center;
		margin-top: 30upx;
	}
</style>
