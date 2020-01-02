<template>
	<view class="content">
		<view class="ul">
			<view class="li">
				<view class="data">
					<text>1</text>位
				</view>
				<view class="fte">
					已激活会员
				</view>
			</view>
			<view class="li">
				<view class="data">
					<text>0</text>分
				</view>
				<view class="fte">
					已获积分
				</view>
			</view>
			<view class="li">
				<view class="data">
					<text>1</text>元
				</view>
				<view class="fte">
					已获奖励
				</view>
			</view>
		</view>
		<view class="navbar">
			<view :class="currentNavitem==0?'nav-item active':'nav-item'" @click="switchNav(0)">
				未激活
			</view>
			<view :class="currentNavitem==1?'nav-item active':'nav-item'" @click="switchNav(1)">
				已激活
			</view>
			<view :class="currentNavitem==2?'nav-item active':'nav-item'" @click="switchNav(2)">
				推荐失败
			</view>
		</view>
		<view class="switchBox" v-if="currentNavitem ==0 || currentNavitem ==1 || currentNavitem ==2">
			<view class="li">
				<view class="left">
					<view class="tel">
						13912345678 <text class="bt ewm">二维码</text>
					</view>
					<text class="date">推荐日期 2019-12-04</text>
				</view>
				<text class="right">推荐生效</text>
			</view>
			<view class="li">
				<view class="left">
					<view class="tel">
						13912345678 <text class="bt sms">短信</text>
					</view>
					<text class="date">推荐日期 2019-12-04</text>
				</view>
				<text class="right">推荐生效</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return {
				currentNavitem:0
			}
		},
		methods:{
			switchNav(val){
				this.currentNavitem = val
			}
		}
	}
</script>

<style lang="less" scoped>
	page {
		background-color: #f7f8fa;
	}
	.ul{
		display: flex;
		align-items: center;
		justify-content: space-between;
		background: #FFFFFF;
		margin-bottom: 20upx;
		padding: 28upx 30upx;
		.li{
			flex: 1;
			text-align: center;
			position: relative;
			&:before{
				content: "";
				height: 100%;
				width: 1px;
				background: #ebebeb;
				position: absolute;
				right: 0;
			}
			&:last-child:before{
				display: none;
			}
			.data{
				font-size: 24upx;
				color: #999999;
				margin-bottom: 8upx;
				text{
					font-size: 32upx;
					color: #ff7f66;
					padding-right: 6upx;
				}
			}
			.fte{
				font-size: 24upx;
				color: #333;
			}
		}
	}
	.navbar{
		display: flex;
		align-items: center;
		justify-content: space-between;
		height: 85upx;
		line-height: 85upx;
		background: #FFFFFF;
		.nav-item{
			flex: 1;
			text-align: center;
			color: #999999;
			font-size: 28upx;
			position: relative;
			&.active{
				color: #333;
			}
			&.active:before{
				position: absolute;
				content: "";
				height: 2px;
				width: 45upx;
				background: #0DB983;
				bottom: 10upx;
				left: 50%;
				transform: translateX(-50%);
			}
		}
	}
	.switchBox{
		.li{
			display: flex;
			align-items: center;
			justify-content: space-between;
			background: #FFFFFF;
			padding: 28upx 30upx;
			position: relative;
			font-size: 28upx;
			color: #333;
			&:before{
				content: "";
				position: absolute;
				left: 30upx;
				right: 30upx;
				bottom: 0;
				height: 1px;
				background: #ededed;
			}
			&:last-child:before{
				display: none;
			}
			.tel{
				display: flex;
				align-items: center;
				.bt{
					font-size: 22upx;
					padding: 4upx 20upx;
					border-radius: 30upx;
					margin-left: 20upx;
				}
				.ewm{
					background: #eaf5ff;
					color: #3399ff;
				}
				.sms{
					background: #e6f8f2;
					color: #79d8ba;
				}
			}
			.date{
				font-size: 24upx;
				color: #999999;
				margin-top: 12upx;
			}
		}
	}
</style>
