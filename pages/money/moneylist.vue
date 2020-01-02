<template>
	<view class="container">
		<view class="li" v-for="item in 8" :key="item">
			<view class="header">
				2019年12月
			</view>
			<view class="list">
				<view class="item">
					<view class="content-box">
						<view class="des-box">
							<view class="tit">转入账户-微信支付</view>
							<view class="time">12-09  16:44</view>
						</view>
					</view>
					<view class="money add">
						+￥158.00
					</view>
				</view>
				<view class="item">
					<view class="content-box">
						<view class="des-box">
							<view class="tit">转入账户-微信支付</view>
							<view class="time">12-09  16:44</view>
						</view>
					</view>
					<view class="money add">
						+￥158.00
					</view>
				</view>
				<view class="item">
					<view class="content-box">
						<view class="des-box">
							<view class="tit">积分兑换-抵扣现金</view>
							<view class="time">12-09  16:44</view>
						</view>
					</view>
					<view class="money integral">
						+1000.00
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return{
				
			}
		},
		methods:{
			
		}
	}
</script>

<style lang="less">
	page {
		background-color: #f7f8fa;
	}
	.header{
		height: 75upx;
		line-height: 75upx;
		font-size: 28upx;
		padding: 0 30upx;
		box-sizing: border-box;
	}
	.list{
		.item{
			width: 100%;
			padding: 30rpx 28rpx;
			box-sizing: border-box;
			background: #fff;
			display: flex;
			align-items: flex-start;
			justify-content: space-between;
			.content-box {
				display: flex;
				align-items: flex-start;
				justify-content: space-between;
				.des-box {
					box-sizing: border-box;
					vertical-align: top;
					color: #333;
					font-size: 24rpx;
					display: flex;
					flex-direction: column;
					justify-content: space-between;
				}
				
				.tit {
					font-size: 32rpx;
					max-width: 420rpx;
					white-space: nowrap;
					overflow: hidden;
					text-overflow: ellipsis;
					margin-bottom: 24upx;
				}
				
				.time {
					color: #888
				}
			}
			
			.money {
				font-size: 38rpx;
				font-weight: 500;
				color: #000;
				white-space: nowrap;
				overflow: hidden;
				text-overflow: ellipsis;
				padding-left: 20rpx;
			}
			
			.add {
				color: #f59d31;
			}
			// 积分的class
			.integral{
				color: #333;
			}
		}
	}
</style>
