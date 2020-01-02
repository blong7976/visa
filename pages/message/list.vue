<template>
	<view class="content">
		<view class="navbar">
			<view :class="currentNavitem==0?'nav-item active':'nav-item'" @click="switchNav(0)">
				订单消息
			</view>
			<view :class="currentNavitem==1?'nav-item active':'nav-item'" @click="switchNav(1)">
				活动消息
			</view>
			<view :class="currentNavitem==2?'nav-item active':'nav-item'" @click="switchNav(2)">
				系统消息
			</view>
		</view>
		
		<view class="ul" v-if="currentNavitem ==0">
			
			<view class="li">
				<!-- <view class="left">
					<image src="../../static/image/icon_word.png" mode=""></image>
				</view> -->
				<view class="right">
					<view class="title">
						欧铁美食水晶世界-法瑞德意11天 [法签]-夜机出行通知书.doc 
					</view>
					<view class="foot">
						<text class="date">2019-12-07</text>
						<text class="btn play">前往支付</text>
					</view>
				</view>
			</view>
			
			<view class="li">
				<view class="left">
					<image src="../../static/image/icon_word.png" mode=""></image>
				</view>
				<view class="right">
					<view class="title">
						欧铁美食水晶世界-法瑞德意11天 [法签]-夜机出行通知书.doc 
					</view>
					<view class="foot">
						<text class="date">2.3 MB | 2019-12-07</text>
						<text class="btn havedownload">已下载</text>
					</view>
				</view>
			</view>
			
			<view class="li">
				<view class="left">
					<image src="../../static/image/icon_pdf.png" mode=""></image>
				</view>
				<view class="right">
					<view class="title">
						澳新8天出团通知书.pdf  
					</view>
					<view class="foot">
						<text class="date">4.5 MB | 2019-12-07</text>
						<text class="btn download">下载</text>
					</view>
				</view>
			</view>
			
		</view>
		
		
		<view class="ul" v-if="currentNavitem ==1">
			<view class="li" v-for="item in 3" :key="item" @click="navTo('/pages/message/details')">
				<view class="right">
					<view class="title">
						周年庆典，充值优惠活动来啦~ <br>充800抵1000，还有积分可以获得哦
					</view>
					<view class="foot">
						<text class="date">2019-12-07</text>
					</view>
				</view>
				<view class="move">
					<image src="../../static/image/icon_more3.png" mode=""></image>
				</view>
			</view>
		</view>
		
		
		<view class="ul" v-if="currentNavitem ==2">
			<view class="li" v-for="item in 2" :key="item">
				<view class="right">
					<view class="title">
						礼品兑换区礼品更新啦，大波好礼来袭，快去兑换先到先得
					</view>
					<view class="foot">
						<text class="date">2019-12-07</text>
					</view>
				</view>
				<view class="move">
					<image src="../../static/image/icon_more3.png" mode=""></image>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return {
				currentNavitem:0,
			}
		},
		methods:{
			navTo(url){
				uni.navigateTo({  
					url
				})  
			}, 
			switchNav(val){
				this.currentNavitem = val
			}
		}
	}
</script>

<style lang="less" >
	page {
		background: #f7f8fa;
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
	.ul{
		padding: 20upx 30upx;
		.li{
			background: #FFFFFF;
			display: flex;
			justify-content: space-between;
			padding: 28upx;
			border-radius: 15upx;
			margin-bottom: 20upx;
			.left{
				width: 55upx;
				height: 58upx;
				margin-right: 20upx;
				margin-top: 10upx;
				image{
					width: 100%;
					height: 100%;
					display: block;
				}
			}
			.right{
				flex: 1;
				.title{
					height: 76upx;
					font-size: 28upx;
					color: #333333;
					display: -webkit-box;
					-webkit-box-orient: vertical;
					-webkit-line-clamp: 2;
					overflow: hidden;
				}
				.foot{
					display: flex;
					align-items: center;
					justify-content: space-between;
					.date{
						font-size: 24upx;
						color: #999999;
					}
					.btn{
						font-size: 24upx;
						color: #333333;
						padding: 6upx 20upx;
						border-radius: 30upx;
						border: 1px solid;
					}
					// 去支付
					.play{
						color: #ff7f66;
						border-color: #ff7f66;
					}
					// 已下载
					.havedownload{
						background: #0db983;
						color: #FFFFFF;
						border-color: #0db983;
					}
					// 下载
					.download{
						color: #0db983;
						border-color: #0db983;
					}
				}
			}
			
			.move{
				width: 70upx;
				text-align: right;
				display: flex;
				align-items: center;
				justify-content: flex-end;
				image{
					width: 12upx;
					height: 22upx;
				}
			}
		}		
	}
</style>
