<template>
	<view class="content">
		<image src="../../static/image/img_fail.png" mode="aspectFill"></image>
		<view class="msg">
			推荐失败
		</view>
		<view class="laber">
			以下号码已被注册为会员或已被他人推荐，当前不可推荐
		</view>
		<view class="list-cell">
			<view class="li">
				<text>被推荐号码</text><text>失败原因</text>
			</view>
			<view class="li">
				<text>17612345678</text><text>已推荐</text>
			</view>
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
	.laber{
		font-size: 24upx;
		color: #ff7f66;
		text-align: center;
		margin-top: 90upx;
	}
	.list-cell{
		background: #FFFFFF;
		border-radius: 15upx;
		margin:30upx;
		.li{
			display: flex;
			align-items: center;
			justify-content: space-between;
			font-size: 28upx;
			color: #333333;
			line-height: 88upx;
			border-bottom: 1px solid #ebebeb;
			padding: 0 30upx;
			&:last-child{
				border: none;
			}
		}
	}
</style>
