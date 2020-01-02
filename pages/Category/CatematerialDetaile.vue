<template>
	<view class="content">
		<view class="alert">
			根据申请人身份类别，签证所需资料可能会有区别
		</view>
		<view class="collapse">
			<view class="panel" v-for="(item,index) in material" :key="index">
				<view class="collapse-header">
					<view class="left-aside">
						{{item.title + '('+item.laber+')'}}
					</view>
					<view class="right-aside" v-if="item.btn" @click="handleClickItem(item)">
						{{item.btn}}
						<!-- <image src="../../static/image/icon_down.png" mode="" :class="item.isShow?'show':''"></image> -->
					</view>
				</view>
				<view class="collapse-content" v-if="item.isShow">
					<view class="cn">
						<text>1.护照离出发日必须有6个月以上有效期</text>
						<text>2.请拍摄上传彩色的护照首页，字体清晰可见，无反光，无遮挡，具体“查看样例”</text>
					</view>
					<text class="see">查看样例</text>
				</view>
			</view>
		</view>
		<view class="flex-box-bottom">
			<view class="btn" @click="emailModalShow= true"><image src="../../static/image/icon_email.png" mode="aspectFit"></image>发送至邮箱</view>
			<view class="btn" @click="shareModalShow= true"><image src="../../static/image/icon_share_white_s.png" mode="aspectFit"></image>分享资料清单</view>
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
						<view class="ul">
							<view :class="currentItem == index?'li active':'li'" v-for="(item,index) in list" :key="item" @click="selectItem(index)">
								{{item}}
							</view>
						</view>
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
		
		<!-- 分享弹窗 -->
		<view class="modal share" v-if="shareModalShow">
			<view class="modal-dialog ">
				<view class="modal-content">
					<view class="modal-header">
						分享 [在职人员] 资料清单至
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
				material:[
					{title:'护照',content:'',laber:'首页',isShow:true,btn:'样例'},
					{title:'照片',content:'',laber:'原件',isShow:false},
					{title:'居住证',content:'',laber:'原件',isShow:false},
					{title:'结婚证',content:'',laber:'复印件',isShow:false},
					{title:'在职证明',content:'',laber:'原件',isShow:true,btn:'模板'},
					{title:'银行流水',content:'',laber:'复印件盖章',isShow:false},
					{title:'营业执照',content:'',laber:'复印件盖公章',isShow:false},
					{title:'辅助材料',content:'',laber:'原件',isShow:false}
				],
				allshow:false,
				list:["在职人员","自由职业者","退休人员","在校学生","学龄前儿童"],
				currentItem:0,
				emailModalShow:false,
				shareModalShow:false
			}
		},
		methods:{
			handleClickItem(i){
				if(i.btn === '模板'){
					uni.navigateTo({
						url:'/pages/Category/Cateprove'
					})
				}
			},
			selectItem(index){
				this.currentItem = index
			}
		}
	}
</script>

<style lang="less" scoped>
	.content{
		padding-bottom: 120upx;
	}
	.alert{
		background: #f7f8fa;
		font-size: 24upx;
		color: #999999;
		line-height: 70upx;
		border-radius: 6upx;
		position: relative;
		padding-left: 80upx;
		border-bottom: 1px solid #ebebeb;
		&:before{
			content: "";
			width: 30upx;
			height:30upx;
			background: url(../../static/image/icon_tip_blue.png) repeat;
			background-size: 100%;
			position: absolute;
			left: 40upx;
			top: 50%;
			transform: translateY(-50%);
		}
	}
	.collapse{
		padding: 0 30upx;
		.panel{
			border-bottom: 1px solid #ebebeb;
			.collapse-header{
				display: flex;
				align-items: center;
				justify-content: space-between;
				font-size: 28upx;
				color: #000;
				padding: 30upx 0;
				.left-aside{
					&:after{
						content: "*";
						color: #ff7f66;
						font-size: 24upx;
						padding-left: 10upx;
					}
				}
				.right-aside{
					display: flex;
					align-items: center;
					color: #555555;
					font-size: 24upx;
					color: #0DB983;
					border: 1px solid #0DB983;
					padding: 5upx 20upx;
					border-radius: 6upx;
					image{
						width: 24upx;
						height: 13upx;
						margin-left: 15upx;
						position: relative;
						transform: rotate(-90deg);
						&.show{
							transform: rotate(0deg);
						}
					}
				}
			}
			&:last-child{
				border: none;
			}
			.collapse-content{
				padding-bottom: 28upx;
				.cn{
					font-size: 28upx;
					color: #999999;
					line-height: 44upx;
				}
				.see{
					font-size: 28upx;
					color: #0db983;
				}
			}
		}
		.foot{
			height: 98upx;
			line-height: 98upx;
			display: flex;
			align-items: center;
			justify-content: center;
			font-size: 28upx;
			color: #333333;
			image{
				width: 22upx;
				height: 12upx;
				position: relative;
				transform: rotate(-90deg);
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
