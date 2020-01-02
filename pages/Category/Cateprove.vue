<template>
	<view class="content">
		<view class="cn">
			在职证明内容区
		</view>
		<view class="flex-box-bottom">
			<view class="btn" @click="shareModalShow= true"><image src="../../static/image/icon_share_white_s.png" mode="aspectFit"></image>分享模板</view>
			<view class="btn" ><image src="../../static/image/icon_download.png" mode="aspectFit"></image>下载模板</view>
		</view>
		
		<!-- 分享弹窗 -->
		<view class="modal share" v-if="shareModalShow">
			<view class="modal-dialog ">
				<view class="modal-content">
					<view class="modal-header">
						分享 [在职人员] 模板至
						<image src="../../static/image/icon_close.png" mode="aspectFit" class="close" @click="shareModalShow = false"></image>
					</view>
					<view class="modal-body">
						<view class="sharelist">
							<view class="item">
								<image src="../../static/image/icon_WX_bg.png" mode="aspectFit"></image>
								<view>微信</view>
							</view>
							<view class="item">
								<image src="../../static/image/icon_qq_bg.png" mode="aspectFit"></image>
								<view>QQ</view>
							</view>
							<view class="item" @click="shareEmail">
								<image src="../../static/image/icon_email_big.png" mode="aspectFit"></image>
								<view>邮箱</view>
							</view>
						</view>
					</view>
				</view>		
			</view>
		</view>
		
		<!-- 发送邮件弹窗 -->
		<view class="modal" v-if="emailModalShow">
			<view class="modal-dialog">
				<view class="modal-content">
					<view class="modal-header">
						发送至邮件
						<image src="../../static/image/icon_close.png" mode="aspectFit" class="close" @click="emailModalShow=false"></image>
					</view>
					<view class="modal-body">
						<input type="email" value="" placeholder="请输入邮箱信息" class="email"/>
						<view class="btn">
							发送邮件
						</view>
						<view class="msg">
							请留意来自szcits@139.com的邮件
						</view>
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
				shareModalShow:false,
				emailModalShow:false
			}
		},
		methods:{
			shareEmail(){
				this.shareModalShow = false
				this.emailModalShow = true
			}
		}
	}
</script>

<style lang="less" scoped>
	.cn{
		position: absolute;
		width: 100%;
		height:calc(100% - 52px);
		display: flex;
		align-items: center;
		text-align: center;
		justify-content: center;
		font-size: 32upx;
	}
	.flex-box-bottom{
		position: fixed;
		bottom: 0;
		left: 0;
		right: 0;
		padding: 10upx 45upx;
		background: #FFFFFF;
		z-index: 99;
		display: flex;
		align-items: center;
		justify-content: space-between;
		.btn{
			height: 84upx;
			line-height: 84upx;
			border-radius: 42upx;
			text-align: center;
			font-size: 32upx;
			flex: 1;
			background:#0db983;
			color: #fff;
			margin-left: 30upx;
			display: flex;
			align-items: center;
			justify-content: center;
			&:first-child{
				margin-left: 0;
			}
			image{
				width: 34upx;
				margin-right: 10upx;
			}
		}
	}
	
	
	
	.modal{
		position: fixed;
		top: 0;
		left: 0;
		z-index: 1050;
		width: 100%;
		height: 100%;
		overflow: hidden;
		background: rgba(0,0,0,.4);
		display: flex;
		align-items: center;
		padding: 0 40upx;
		box-sizing: border-box;
		.modal-dialog{
			position: relative;
			flex: 1;
			background: #FFFFFF;
			border-radius: 15upx;
			.modal-header{
				font-size: 28upx;
				color: #333333;
				text-align: center;
				line-height: 80upx;
				position: relative;
				.close{
					width: 23upx;
					height: 23upx;
					position: absolute;
					right: 40upx;
					top: 50%;
					margin-top: -10upx;
				}
			}
			.modal-body{
				padding: 0 30upx;
				box-sizing: border-box;
				.ul{
					display: flex;
					justify-content: flex-start;
					flex-wrap: wrap;
					.li{
						width: 30%;
						text-align: center;
						font-size: 28upx;
						color: #999999;
						height: 78upx;
						line-height: 78upx;
						border: 1px solid #ebebeb;
						border-radius: 10upx;
						box-sizing: border-box;
						margin-right: 5%;
						text-overflow: ellipsis;
						white-space: nowrap;
						overflow: hidden;
						&:nth-child(3n){
							margin-right: 0;
						}
						&:nth-child(n+4){
							margin-top: 20upx;
						}
						&.active{
							color: #0DB983;
							border-color: #0DB983;
							position: relative;
							&:before{
								content: "";
								background: url(../../static/image/icon_checkbox_pre2.png) no-repeat;
								background-size: 100%;
								width: 28upx;
								height: 28upx;
								position: absolute;
								top: 0;
								right: 0;
							}
						}
					}
				}
				.email{
					font-size: 28upx;
					color: #555555;
					border: 1px solid #ebebeb;
					border-radius: 10upx;
					line-height: 98upx;
					height: 98upx;
					margin: 20upx 0;
					padding: 0 30upx;
				}
				.btn{
					height: 84upx;
					line-height: 84upx;
					border-radius: 42upx;
					text-align: center;
					font-size: 32upx;
					width: 100%;
					background:#0db983;
					color: #fff;
				}
				.msg{
					font-size: 28upx;
					color: #999;
					margin: 30upx 0;
					text-align: center;
				}
			}
		}
	
	}
	.share{
		padding: 0;
		.modal-dialog{
			position: absolute;
			bottom: 0;
			width: 100%;
			border-radius: 0;
			border-top-left-radius: 30upx;
			border-top-right-radius: 30upx;
			.sharelist{
				padding: 58upx 0;
				display: flex;
				justify-content: space-between;
				align-items: center;
				.item{
					flex: 1;
					text-align: center;
					font-size: 28upx;
					color: #333333;
					image{
						width: 100upx;
						height: 100upx;
					}
				}
			}
		}
	}
</style>
