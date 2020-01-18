<template>
	<view class="content">
		<view class="item" v-for="(item ,index) in list" :key="index" :style="{background:item.color}">
			<view class="icon">
				<image :src="item.icon" mode="aspectFit"></image>
			</view>
			<view class="cn">
				<view class="title">{{item.name}}</view>
				<view class="p">{{item.code}}</view>
			</view>
		</view>
		<view class="add" @click="navTo('/pages/money/BankcardCode')">
			<image src="../../static/image/icon_add2.png"></image>添加银行卡
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				list:[{
					name:'建设银行',
					code:'**** **** **** 0780',
					icon:'../../static/image/icon_jianshe2.png',
					color:'#0066b3'
				},{
					name:'农业银行',
					code:'**** **** **** 0780',
					icon:'../../static/image/icon_nongye2.png',
					color:'#009174'
				}]
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
	page{
		background: #f7f8fa;
	}
	.content{
		padding: 0 30upx;padding-top: 20upx;
		.item{
			margin-bottom: 20upx;
			padding:40upx 30upx;
			border-radius: 10upx;
			overflow: hidden;
			display: flex;
			justify-content: space-between;
			color: #FFFFFF;
			.icon{
				width: 64upx;
				height: 64upx;
				background: #FFFFFF;
				border-radius: 50%;
				overflow: hidden;
				display: flex;
				align-items: center;
				justify-content: center;
				image{
					width: 44upx;height: 44upx;display: block;
				}
			}
			.cn{
				flex: 1;
				padding-left: 24upx;
				.title{
					line-height: 64upx;
					font-size: 30upx;
				}
				.p{
					padding-top: 20upx;
					font-size: 40upx;
				}
			}
		}
		.add{
			font-size: 30upx;
			color: #333333;
			display: flex;
			align-items: center;
			image{
				width: 36upx;height: 36upx;margin-right: 20upx;
			}
		}
	}
</style>
