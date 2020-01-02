<template>
	<view class="content">
		<view class="navbar">
			<view :class="currentNavitem==0?'nav-item active':'nav-item'" @click="switchNav(0)">
				二维码推荐
			</view>
			<view :class="currentNavitem==1?'nav-item active':'nav-item'" @click="switchNav(1)">
				短信推荐
			</view>
		</view>
		<view class="navContent" v-if="currentNavitem==0">
			<view class="alert">
				<image src="../../static/image/icon_horn.png" mode="aspectFill" class="icon"></image>
				推荐一名会员可获得 100 积分，积分可兑"旅行礼品"和"抵团费"使用
			</view>
			<view class="Qrcode">
				<view class="ewm">
					<image src="../../static/image/ewm.png" mode="aspectFill"></image>
				</view>
				<view class="msg">
					长按保存，微信扫码或识码注册
				</view>
			</view>
			<view class="Sendto">
				<view class="title">
					<text class="line"></text>
					<text>分享至</text>
					<text class="line"></text>
				</view>
				<view class="list">
					<view class="item" v-for="item in sharelist" :key="item.name">
						<image :src="item.img" mode="aspectFit"></image>
						<text>{{item.name}}</text>
					</view>
				</view>
			</view>
		</view>
		<view class="navContent" v-if="currentNavitem==1">
			<view class="alert">
				<image src="../../static/image/icon_horn.png" mode="aspectFill" class="icon"></image>
				推荐一名会员可获得 100 积分，积分可兑"旅行礼品"和"抵团费"使用
			</view>
			<view class="list-cell">
				<view class="cell-tit">
					推荐人
				</view>
				<view class="cell-con">
					<input type="text" value="15102988385" />
				</view>
			</view>
			<view class="info">
				<view class="title">
					推荐内容
				</view>
				<view class="select">
					<view class="item">
						<textarea value="" placeholder="请输入推荐内容" v-if="isEdit"/>
						<view class="" v-else>
							轻游记”去旅游性价比很高，值得推荐使用！您的好友15212345678邀请您加入轻游记，点击链接注册，https://www.qiyouji.net/......，
							<text class="color" @click="handleEdit">轻游记”很好，建议您用（蓝色部分可编辑）</text>
						</view>
					</view>
				</view>
			</view>
			<view class="info">
				<view class="title">
					被推荐人
				</view>
				<view class="select">
					<view class="item-input">
						<image src="../../static/image/icon_add.png" mode="" class="icon"></image>
						<input type="text" value="17612345678" />
					</view>
					<view class="item-input">
						<image src="../../static/image/icon_del.png" mode="" class="icon"></image>
						<input type="text" value="" placeholder="请输入被推荐人手机号"/>
					</view>
				</view>
			</view>
			<view class="flex-box-bottom">
				<view class="btn" @click="navTo('/pages/share/shareError')">发送</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default{
		data(){
			return {
				currentNavitem:0,
				sharelist:[{
					img:'../../static/image/share1.png',
					name:'微信'
				},{
					img:'../../static/image/share2.png',
					name:'朋友圈'
				},{
					img:'../../static/image/share3.png',
					name:'QQ'
				},{
					img:'../../static/image/share4.png',
					name:'微博'
				},{
					img:'../../static/image/share5.png',
					name:'抖音'
				},{
					img:'../../static/image/share6.png',
					name:'钉钉'
				}],
				isEdit:false
			}
		},
		mounted() {
			this.isEdit = false
		},
		methods:{
			// #ifndef MP
			onNavigationBarButtonTap(e) {
				const index = e.index;
				if (index === 0) {
					this.navTo('/pages/share/detailes');
				}
			},
			// #endif
			navTo(url){
				uni.navigateTo({  
					url
				})  
			}, 
			switchNav(val){
				this.currentNavitem = val
				if(val == 1){
					this.isEdit = false
				}
			},
			handleEdit(){
				this.isEdit =true
			}
		}
	}
</script>

<style lang="less">
	page {
		background-color: #f7f8fa;
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
	.navContent{
		padding: 0 30upx;
		.alert{
			padding-top: 20upx;
			font-size: 24upx;
			color: #999;
			line-height: 1.5;
			.icon{
				width: 28upx;
				height: 26upx;
				margin-right: 10upx;
				vertical-align: middle;
			}
		}
		.Qrcode{
			width: 560upx;
			height: 650upx;
			background: #FFFFFF;
			margin: 56upx auto 0;
			border-radius: 15upx;
			padding-top: 70upx;
			position: relative;
			overflow: hidden;
			box-sizing: border-box;
			.ewm{
				width: 400upx;
				height: 400upx;
				background: #e6e6e6;
				margin: 0 auto;
				overflow: hidden;
				image{
					width: 100%;
					height: 100%;
				}
			}
			.msg{
				height: 118upx;
				line-height: 118upx;
				position: absolute;
				bottom: 0;
				left: 0;
				width: 100%;
				text-align: center;
				font-size: 28upx;
				color: #333333;
				border-top: 1px dashed #ebebeb;
				&:before{
					content: "";
					width: 40upx;
					height: 40upx;
					background: #f7f8fa;
					border-radius: 50%;
					position: absolute;
					top: -20upx;
					left: -20upx;
					z-index: 10;
				}
				&:after{
					content: "";
					width: 40upx;
					height: 40upx;
					background: #f7f8fa;
					border-radius: 50%;
					position: absolute;
					top: -20upx;
					right: -20upx;
					z-index: 10;
				}
			}
		}
		
		.Sendto{
			position: fixed;
			bottom: 0;
			left: 0;
			width: 100%;
			z-index: 12;
			.title{
				font-size: 28upx;
				color: #333333;
				display: flex;
				align-items: center;
				justify-content: space-between;
				width: 70%;
				margin: 0 auto;
				text{
					flex: 1;
					text-align: center;
				}
				.line{
					height: 1px;
					display: block;
					background: #ebebeb;
					width: 100%;
				}
			}
			.list{
				display: flex;
				align-items: center;
				justify-content: space-between;
				padding: 35upx 0 40upx;
				.item{
					flex: 1;
					text-align: center;
					font-size: 28upx;
					color: #333333;
					image{
						width: 50upx;
						height: 50upx;
					}
					text{
						display: block;
					}
				}
			}
		}
	
		.list-cell{
			display: flex;
			align-items: center;
			background: #FFFFFF;
			padding: 30upx;
			border-radius: 10upx;
			margin: 25upx 0 20upx;
			font-size: 28upx;
			.cell-tit{
				margin-right: 40upx;
			}
			input{
				font-size: 28upx;
				color: #999999;
			}
		}
	}
	.info{
		background: #FFFFFF;
		border-radius: 15upx;
		margin-bottom: 20upx;
		.title{
			line-height: 90upx;
			height: 90upx;
			font-size: 32upx;
			padding:0 30upx;
			border-bottom: 1px solid #ebebeb;
		}
		.input{
			padding: 0 30upx;
			display: flex;
			height: 128upx;
			line-height: 128upx;
			position: relative;
			&:before{
				content: "￥";
				font-size: 30upx;
				position: relative;
				top: 10upx;
				margin-right: 10upx;
			}
			input{
				font-size: 64upx;
				color: #333333;
				height: 128upx;
				line-height: 128upx;
			}
		}
		.select{
			padding: 20upx 30upx;
			.item{
				line-height: 40upx;
				font-size: 28upx;
				position: relative;
				color: #999999;
				.color{
					color: #3b91e7;
				}
				textarea{
					font-size: 28upx;
				}
			}
			.item-input{
				line-height: 70upx;
				height: 70upx;
				font-size: 28upx;
				display: flex;
				align-items: center;
				position: relative;
				.icon{
					width: 32upx;
					height: 32upx;
					margin-right: 32upx;
				}
				input{
					line-height: 70upx;
					height: 70upx;
					font-size: 28upx;
					flex: 1;
				}
			}
		}
	}
	.flex-box-bottom{
		position: fixed;
		bottom: 0;
		left: 0;
		right: 0;
		padding: 10upx 45upx;
		background: #FFFFFF;
		z-index: 99;
	}
	.btn{
		height: 84upx;
		line-height: 84upx;
		border-radius: 42upx;
		text-align: center;
		font-size: 32upx;
		width: 100%;
		background:#0fb87f;
		color: #fff;
	}
</style>
