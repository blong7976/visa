<template>
	<view :class="exchangeModal?'hiddenbox':''">
		<scroll-view
			class="list-scroll-content" 
			scroll-y
			@scrolltolower="loadData"
		>
			<view
				v-for="(item,index) in list" :key="index"
				class="order-item"
			>
			 <image class="goods-img" :src="item.image" mode="aspectFill"></image>
			 <view class="right">
			 	<text class="title clamp2">{{item.title}}</text>
				<view class="bottom">
					<text class="integral">{{item.integral}}</text>
					<text class="price">{{item.price}}</text>
					<text class="btn" @click="exchange">立即兑换</text>
				</view>
			 </view>
			</view>
			<uni-load-more :status="loadingType"></uni-load-more>
		</scroll-view>
		<!-- 兑换弹窗 -->
		<view class="modal" v-if="exchangeModal">
			<view class="modal-body">
				<image src="../../static/image/exchangeBg.png" mode=""></image>
				<view class="close" @click="closeModal"></view>
				<view class="content">
					<text class="h1">成功兑换礼品</text>
					<text class="msg">邮寄地址可到 [我的订单] 中更改</text>
					<view class="btn">
						查看礼品订单
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import uniLoadMore from '@/components/uni-load-more/uni-load-more.vue';
	export default {
		components: {
			uniLoadMore,
		},
		data(){
			return {
				loadingType:'more',
				list:[],
				exchangeModal:false
			}
		},
		onLoad(options){
			this.loadData()
		},
		methods:{
			loadData(){
				this.loadingType = 'loading';
				setTimeout(()=>{
					let newlist = [
						{
							image:'../../static/image/icon_chat.png',
							title:'小米充电宝20000毫安大容量便携超薄支持双向PD快充',
							integral:'2000',
							price:'200'
						},{
							image:'../../static/image/icon_chat.png',
							title:'小米充电宝20000毫安大容量便携超薄支持双向PD快充',
							integral:'2000',
							price:'200'
						},{
							image:'../../static/image/icon_chat.png',
							title:'小米充电宝20000毫安大容量便携超薄支持双向PD快充',
							integral:'2000',
							price:'200'
						},{
							image:'../../static/image/icon_chat.png',
							title:'小米充电宝20000毫安大容量便携超薄支持双向PD快充',
							integral:'2000',
							price:'200'
						},{
							image:'../../static/image/icon_chat.png',
							title:'小米充电宝20000毫安大容量便携超薄支持双向PD快充',
							integral:'2000',
							price:'200'
						},{
							image:'../../static/image/icon_chat.png',
							title:'小米充电宝20000毫安大容量便携超薄支持双向PD快充',
							integral:'2000',
							price:'200'
						},{
							image:'../../static/image/icon_chat.png',
							title:'小米充电宝20000毫安大容量便携超薄支持双向PD快充',
							integral:'2000',
							price:'200'
						}
					]
					this.list = this.list.concat(newlist)
					this.loadingType = 'more';
				}, 600);
			},
			exchange(){
				uni.showLoading({
					title:'请求中'
				})
				setTimeout(()=>{
					uni.hideLoading()
					this.exchangeModal = true
				},600)
			},
			closeModal(){
				this.exchangeModal = false
			}
		}
	}
</script>

<style lang="less">
	page{
		background: #f7f8fa;
	}
	.hiddenbox{
		overflow: hidden;
	}
	.list-scroll-content{
		padding-bottom: 20upx;
	}
	.order-item{
		margin:20upx 30upx 0 30upx;
		background: #FFFFFF;
		border-radius: 10px;
		box-sizing: border-box;
		padding: 30upx 22upx;
		display: flex;
		.goods-img{
			width: 140upx;
			height: 140upx;
			display: block;
			background: #fafafa;
		}
		.right{
			flex: 1;
			display: flex;
			flex-direction: column;
			padding-left: 24upx;
			overflow: hidden;
			.title{
				font-size: 28upx;
				color: #000;
				line-height: 40upx;
			}
			.bottom{
				margin-top: 20upx;
				.integral{
					font-size: 32upx;
					color: #ff7f66;
					font-weight: bold;
					&:before{
						content: '积分';
						font-weight: 400;
						font-size: 24upx;
						margin: 0 2upx 0 8upx;
					}
				}
				.price{
					font-size: 24upx;
					color: #b2b2b2;
					text-decoration:line-through;
					&:before{
						content: '￥';
						font-size: 24upx;
						margin: 0 2upx 0 8upx;
					}
				}
				.btn{
					font-size: 24upx;
					color: #0db983;
					float: right;
					width: 140upx;
					height: 44upx;
					line-height: 44upx;
					border: 1px solid #0db983;
					border-radius: 22upx;
					text-align: center;
					cursor: pointer;
				}
			}
		}
	}
	
	.modal{
		position: fixed;
		top:0;
		left:0;
		bottom:0;
		right: 0;
		background: rgba(0,0,0,.5);
		z-index: 999;
		.modal-body{
			position: fixed;
			left: 50%;
			top: 50%;
			margin: auto;
			background: #fff;
			z-index: 9999;
			transition: all 0.3s ease-in-out;
			box-sizing: border-box;
			transform: translate(-50%, -50%) scale(1);
			width: 560upx;
			height: 590upx;
			border-radius: 10px;
			image{
				width: 100%;
				height: 100%;
			}
			.close{
				width: 30upx;
				height: 30upx;
				position: absolute;
				top: 30upx;
				right: 30upx;
			}
			.content{
				position: absolute;
				top: 250upx;
				width: 100%;
				text-align: center;
				text{
					display: block;
				}
				.h1{
					font-size: 40upx;
					margin-top: 75upx;
				}
				.msg{
					font-size: 24upx;
					color: #999999;
					margin-top: 50upx;
				}
				.btn {
				  background-color: rgb(255, 127, 102);
				  width: 380upx;
				  height: 72upx;
				  text-align: center;
				  line-height: 72upx;
				  border-radius: 36upx;
				  margin: 0 auto;
				  margin-top: 23upx;
				  color: #FFFFFF;
				  font-size: 32upx;
				}

			}
		}
	}

</style>
