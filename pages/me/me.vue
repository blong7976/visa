<template>
	<view class="content">
		
		<view class="user-section">
			<image class="bg" src="../../static/image/mebgImg.png"></image>

			<view class="tui-header-center" :style="{top:tops+'rpx'}">
				<image src="../../static/image/user.png" class="tui-avatar" mode="widthFix"></image>
				<view class="tui-info">
					<view class="tui-nickname" @click="navTo('/pages/userinfo/userinfo')">易只咩<image src="/static/image/icon_more_w_s.png" class="tui-img-move"></image>
					</view>
					<view class="tui-explain">个人会员</view>
				</view>
				<view class="tui-btn-edit">
					<image src="../../static/image/icon_qrcode.png" mode=""></image>
				</view>
			</view>
			
			<view class="order-section">
				<view class="order-item" @click="navTo('/pages/message/list')" hover-class="common-hover"  :hover-stay-time="50">
					<view class="yticon">
						<text class="number">56</text>
						<image src="../../static/image/icon_message.png" mode="aspectFill"></image>
					</view>
					<text>我的消息</text>
				</view>
				<view class="order-item" @click="navTo('/pages/ShoppingCart/orderlist')"  hover-class="common-hover" :hover-stay-time="50">
					<view class="yticon">
						<image src="../../static/image/icon_order.png" mode="aspectFill"></image>
					</view>
					<text>我的订单</text>
				</view>
				<view class="order-item" @click="navTo('/pages/money/money')" hover-class="common-hover"  :hover-stay-time="50">
					<view class="yticon">
						<image src="../../static/image/icon_wallet.png" mode="aspectFill"></image>
					</view>
					<text>我的钱包</text>
				</view>
				<view class="order-item" @click="navTo('/pages/share/share')" hover-class="common-hover"  :hover-stay-time="50">
					<view class="yticon">
						<image src="../../static/image/icon_recommend.png" mode="aspectFill"></image>
					</view>
					<text>分享推荐</text>
				</view>
			</view>
		</view>
		
		
		<view class="cover-container">
			<view class="ul-section">
				<view class="list-cell" @click="navTo('/pages/invoice/invoicelist')">
					<image class="cell-icon" src="../../static/image/icon_invoice.png"></image>
					<text class="cell-tit">我的发票</text>
					<text class="cell-more yticon icon-you"></text>
				</view>
				<view class="list-cell" @click="navTo('/pages/address/address')">
					<image class="cell-icon" src="../../static/image/icon_address.png"></image>
					<text class="cell-tit">地址管理</text>
					<text class="cell-more yticon icon-you"></text>
				</view>
			</view>
			<view class="ul-section">
				<view class="list-cell" @click="navTo('/pages/collect/collect')">
					<image class="cell-icon" src="../../static/image/icon_collect.png"></image>
					<text class="cell-tit">我的收藏</text>
					<text class="cell-more yticon icon-you"></text>
				</view>
				<view class="list-cell" @click="navTo('/pages/gift/gift')">
					<image class="cell-icon" src="../../static/image/icon_gift.png"></image>
					<text class="cell-tit">我的礼品</text>
					<text class="cell-more yticon icon-you"></text>
				</view>
			</view>
			<view class="ul-section">
				<view class="list-cell">
					<image class="cell-icon" src="../../static/image/icon_service2.png"></image>
					<text class="cell-tit">客服中心</text>
					<text class="cell-more yticon icon-you"></text>
				</view>
				<!-- #ifdef MP -->
				<view class="list-cell" @click="navTo('/pages/set/set')">
					<image class="cell-icon" src="../../static/image/icon_classify_pre.png"></image>
					<text class="cell-tit">设置</text>
					<text class="cell-more yticon icon-you"></text>
				</view>
				<!-- #endif -->
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: '我的',
				top:0,
				height:64,
				tops:120
			}
		},
		async onLoad(options){
			let obj = {};
			// #ifdef MP-WEIXIN
			obj = wx.getMenuButtonBoundingClientRect();
			// #endif
			// #ifdef MP-BAIDU
			obj = swan.getMenuButtonBoundingClientRect();
			// #endif
			// #ifdef MP-ALIPAY
			my.hideAddToDesktopMenu();
			// #endif
			setTimeout(() => {
				uni.getSystemInfo({
					success: (res) => {
						this.height = obj.top ? (obj.top + obj.height + 8) : (res.statusBarHeight + 44);
						this.top = obj.top ? (obj.top + (obj.height - 32) / 2) : (res.statusBarHeight);
						// #ifdef MP
						this.tops = this.top+this.height+15
						// #endif
						
					}
				})
			}, 50)
		},
		methods: {
			navTo(url){
				uni.navigateTo({  
					url
				})  
			}, 
			// #ifndef MP
			onNavigationBarButtonTap(e) {
				const index = e.index;
				if (index === 0) {
					this.navTo('/pages/set/set');
				}
			},
			// #endif
		}
	}
</script>

<style lang="less">
	page {
		background-color: #f7f8fa;
	}
	.user-section{
		height: 600upx;
		position:relative;
		.bg{
			position:absolute;
			left: 0;
			top: 0;
			width: 100%;
			height: 100%;
			filter: blur(1px);
			opacity: .7;
		}
	}
	.user-info-box{
		height: 240upx;
		position:relative;
		z-index: 1;
		top: 110upx;
		text-align: center;
		.portrait{
			width: 130upx;
			height: 130upx;
			border:5upx solid #fff;
			border-radius: 50%;
			margin: 0 auto;
		}
		.username{
			font-size: 40upx;
			color: #fff;
		}
		.edit{
			font-size: 24upx;
			color: #fff;
		}
	}
	
	.cover-container{
		margin: 0 30upx;
		margin-top: -40upx;
		position: relative;
		padding-bottom: 10px;
		min-height: 160upx;
		box-sizing: border-box;
		.ul-section{
			border-radius: 16upx;
			background: #fff;
			margin-bottom: 20upx;
			.list-cell{
				display: flex;
				-webkit-box-align: baseline;
				-webkit-align-items: baseline;
				-ms-flex-align: baseline;
				align-items: baseline;
				padding: 10px 15px;
				line-height: 30px;
				position: relative;
				.cell-icon{
					align-self:center;
					width:32upx;
					max-height:32upx;
					font-size:38upx;
					margin-right: 20upx;
				}
				.cell-more{
					align-self: center;
					font-size:30upx;
					color:#555;
					margin-left:20upx;
				}
				.cell-tit{
					flex: 1;
					font-size: 28upx;
					color: #303133;
					margin-right:10upx;
				}
			}
		}
	}
	
	.tui-header-center {
		position: absolute;
		width: 100%;
		height: 128rpx;
		left: 0;
		top: 120rpx;
		padding: 0 30rpx;
		box-sizing: border-box;
		display: flex;
		align-items: center;
	}
	
	.tui-avatar {
		flex-shrink: 0;
		width: 128rpx;
		height: 128rpx;
		display: block;
		border-radius: 50%;
		border: 2px solid #fff;
		box-sizing: border-box;
	}
	
	.tui-info {
		width: 70%;
		padding-left: 30rpx;
	
	}
	
	.tui-nickname {
		font-size: 30rpx;
		font-weight: 500;
		color: #fff;
		display: flex;
		align-items: center;
	}
	
	.tui-img-move {
		width: 12rpx;
		height: 22rpx;
		margin-left: 18rpx;
	}
	
	.tui-explain {
		width: 80%;
		font-size: 24rpx;
		font-weight: 400;
		color: #fff;
		padding-top: 8rpx;
		white-space: nowrap;
		overflow: hidden;
		text-overflow: ellipsis;
	}
	
	.tui-btn-edit {
		flex-shrink: 0;
		height: 80upx;
		image{
			width: 80upx;
			height: 80upx;
		}
	}
	
	.tui-header-btm {
		width: 100%;
		padding: 0 30rpx;
		box-sizing: border-box;
		position: absolute;
		left: 0;
		top: 280rpx;
		display: flex;
		align-items: center;
		justify-content: space-between;
		color: #fff;
	}
	.order-section{
		position: absolute;
		left: 30upx;
		right: 30upx;
		top: 300rpx;
		padding: 28upx 0;
		display: flex;
		justify-content: space-around;
		align-content: center;
		background: #fff;
		border-radius: 5px;
		.order-item{
			font-size: 28upx;
			color: #333;
		}
		.yticon{
			width: 95upx;
			height: 95upx;
			font-size: 48upx;
			margin: 0 auto;
			margin-bottom: 18upx;
			display: block;
			border: 1px solid #ebebeb;
			border-radius: 50%;
			position: relative;
			display: flex;
			align-items:center;
			justify-content:center;
			image{
				width: 40upx;
				max-height: 40upx;
			}
			.number{
				font-size: 24upx;
				background: #ff7f66;
				height: 28upx;
				line-height: 28upx;
				padding: 0 10upx;
				border-radius: 14upx;
				position: absolute;
				top: 0;
				right: 0;
				color: #fff;
			}
		}
		.icon-shouhoutuikuan{
			font-size:44upx;
		}
	}
</style>
