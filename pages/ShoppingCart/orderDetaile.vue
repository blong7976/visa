<template>
	<view class="content">
		<uni-nav-bar class="navber" left-icon="back" title="订单详情"  fixed backgroundColor="#0db983" color="#fff" :height="height" :top="top" @clickLeft="black">
			<!-- #ifndef MP -->
			<view slot="right" class="rightIcon">
				<image src="../../static/image/icon_service20.png" mode=""></image>
			</view>
			<!-- #endif -->
		</uni-nav-bar>
		
		<view class="tabbody">
			<view class="card">
				<view class="tr">
					<view class="td">
						<image v-if="currentsteps==0" src="../../static/image/icon_provide_pre.png" mode="aspectFit"></image>
						<image v-else src="../../static/image/icon_provide.png" mode="aspectFit"></image>
						<text>提交资料</text>
					</view>
					<view class="td">
						<image v-if="currentsteps==1" src="../../static/image/icon_examine_pre.png" mode="aspectFit"></image>
						<image v-else src="../../static/image/icon_examine.png" mode="aspectFit"></image>
						<text>资料审核</text>
					</view>
					<view class="td">
						<image v-if="currentsteps==2" src="../../static/image/icon_embassy_press.png" mode="aspectFit"></image>
						<image v-else src="../../static/image/icon_embassy.png" mode="aspectFit"></image>
						<text>送签使馆</text>
					</view>
					<view class="td">
						<image v-if="currentsteps==3"  src="../../static/image/icon_signout_press.png" mode="aspectFit"></image>
						<image v-else src="../../static/image/icon_signout.png" mode="aspectFit"></image>
						<text>出签配送</text>
					</view>
				</view>
			</view>
		</view>
		
		<block v-if="currentsteps==0">
		<view class="section">
			<view class="header">
				<text>预计出行日期</text>
				<view class="right" @click="datapackModalShow=true">
					{{date}} <image src="../../static/image/icon_edit_s.png" mode="aspectFit"></image>
				</view>
			</view>
			<view class="body">
				<view class="colorBox">
					请于 <text style="color: #0DB983;">2019年12月29日</text> 前完成签证材料提交，避免耽误您的出行时间
				</view>
			</view>
		</view>
		
		<view class="section">
			<view class="header">
				<text>申请人</text>
				<view class="right">
					共5人
				</view>
			</view>
			<view class="body users">
				<view class="li">
					<view class="add">
						<view class="left">
							<image src="../../static/image/icon_add.png" mode="aspectFit"></image>
							刘北山
						</view>
						<view class="right">
							<text class="btn zwBtn" @click="identityModalShow=true">在职人员<text class="yticon icon-you"></text></text><text class="btn download">资料清单</text>
						</view>
					</view>
					<view class="minus">
						<view class="left">
							<image src="../../static/image/icon_del2.png" mode="aspectFit"></image>
							<input type="text" value="" placeholder="请输入申请人姓名"/>
						</view>
						<view class="right"></view>
					</view>
				</view>
			</view>
		</view>
		
		
		<view class="section">
			<view class="header">
				<text>提交资料方式</text>
				<view class="right">
					长按文本可复制
				</view>
			</view>
			<view class="body">
				<view class="submitway">
					<view class="title">
						在线提交
					</view>
					<view class="colorBox zxType">
						<view class="list">
							<image src="../../static/image/share1.png" mode="aspectFit"></image>tour56789
						</view>
						<view class="list">
							<image src="../../static/image/icon_qq_bg.png" mode="aspectFit"></image>8765432110
						</view>
						<view class="list">
							<image src="../../static/image/icon_email_big.png" mode="aspectFit"></image>qingyouji@139.com
						</view>
					</view>
					<view class="title">
						邮寄地址资料
					</view>
					<view class="colorBox yjType">
						<view class="u-box">
							<image src="../../static/image/icon_location_big.png" mode="aspectFit"></image>
							<text class="name">轻游记官方</text>
							<text class="mobile">18002560061</text>
						</view>
						<view class="address-box">
							<text class="address">广东省深圳市福田区皇岗街道办事处皇岗商务中心55楼滴加有限公司</text>
						</view>
					</view>
				</view>
			</view>
		</view>
	
		</block>
		
		
		<block v-if="currentsteps==1">
			<view class="defaultBox">
				<image src="../../static/image/img_dataaudit.png" mode="aspectFit"></image>
				<view class="msg">
					资料审核中...
				</view>
			</view>
		</block>
		
		<block v-if="currentsteps==2">
			<view class="defaultBox">
				<image src="../../static/image/img_embassy.png" mode="aspectFit"></image>
				<view class="msg">
					送签使馆中...
				</view>
			</view>
		</block>
		
		<block v-if="currentsteps==3">
			<view class="defaultBox">
				<image src="../../static/image/img_express.png" mode="aspectFit"></image>
				<view class="msg">
					{{hasAddress?'出签配送中...':'您还未填写收货地址哦'}}
				</view>
				<view class="btn" v-if="!hasAddress" @click="navTo('/pages/address/address')">
					添加地址
				</view>
			</view>
		</block>
		
		<view class="section">
			<view class="header">
				<text>签证商品</text>
				<view class="right">
				</view>
			</view>
			<view class="body">
				<view class="goods-item" @click="navTo('/pages/Category/CategoryDetaile')">
					<view class="wrapper">
						<view class="u-box">
							<text class="name">日本一个月单次旅游签证</text>
						</view>
						<view class="address-box">
							<text class="attr attr-blue">电子签</text>
						</view>
					</view>
					<text class="yticon icon-you"></text>
				</view>
			</view>
		</view>
		
		
		
		<!-- 切换申请人身份 -->
		<view class="modal share" v-if="identityModalShow">
			<view class="modal-dialog ">
				<view class="modal-content">
					<view class="modal-header">
						切换申请人身份
						<image src="../../static/image/icon_close.png" mode="aspectFit" class="close" @click="identityModalShow = false"></image>
					</view>
					<view class="modal-lab">
						根据申请人身份类别，签证所需资料可能会有区别
					</view>
					<view class="modal-body">
						<view class="sharelist">
							<view :class="currentid==index?'item active':'item'" 
									v-for="(item,index) in identitylist" :key="item.title"
									@click="identitySelect(index)"
									>
								<view class="left">
									{{item.title}}
								</view>
								<view class="right">
									{{item.laber}}
								</view>
							</view>
						</view>
					</view>
				</view>		
			</view>
		</view>
		
		<!-- 选择预计出行日期 -->
		<view class="modal share" v-if="datapackModalShow">
			<view class="modal-dialog ">
				<view class="modal-content">
					<view class="modal-header">
						选择预计出行日期
						<image src="../../static/image/icon_close.png" mode="aspectFit" class="close" @click="datapackModalShow = false"></image>
					</view>
					<view class="modal-lab">
						签证具备有效期，请点击下方按钮选择预计出行日期，以便为您匹配最佳办签时间
					</view>
					<view class="modal-body dateCalendar">
						<uni-calendar  @change="change" @monthSwitch="monthSwitch" />
					</view>
				</view>		
			</view>
		</view>
		
	</view>
</template>

<script>
	import uniNavBar from "@/components/uni-nav-bar/uni-nav-bar.vue";
	import luBarTabNav from "@/components/lu-bar-tab-nav/lu-bar-tab-nav.vue";
	import uniCalendar from '@/components/uni-calendar/uni-calendar.vue';
	export default{
		components: {uniNavBar,luBarTabNav,uniCalendar},
		data(){
			return{
				top:0,
				height:64,
				currentsteps:0,
				hasAddress:false,//出签配送判断是否有配送地址
				identityModalShow:false,
				identitylist:[{
					title:'在职人员',
					laber:'企业、事业单位员工'
				},{
					title:'自由职业者',
					laber:'自由职业、个体经营者'
				},{
					title:'退休人员',
					laber:'退休、离休人员'
				},{
					title:'在校学生',
					laber:'在校学生'
				},{
					title:'学龄前儿童',
					laber:'学龄前儿童'
				}],
				currentid:0,
				datapackModalShow:false,
				date:'2019-12-28'
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
					}
				})
			}, 50)
		},
		methods:{
			navTo(url){
				uni.navigateTo({
					url
				})
			},
			black(){
				uni.navigateBack();
			},
			identitySelect(index){
				this.currentid = index
				setTimeout(()=>{
					this.identityModalShow = false
				},300)
			},
			change(e) {
				// console.log('change 返回:', e)
				if(e){
					this.date = e.fulldate
					setTimeout(()=>{
						this.datapackModalShow = false
					},300)
				}
			},
			monthSwitch(e) {
				// console.log('monthSwitchs 返回:', e)
			}
		}
	}
</script>

<style lang="less" >
	page{
		background: #f7f8fa;padding-bottom: 120upx;
	}
	.yticon{font-size: 24upx;}
	/deep/.uni-navbar__header-btns{
		width: auto;
	}
	.rightIcon{
		position: absolute;
		right: 30upx;
		image{
			width: 45upx;
			height: 45upx;
			float: left;
			padding-right: 20upx;
			&:last-child{
				padding-right: 0;
			}
		}
	}
	
	.tabbody{
		box-sizing: border-box;
		.card{
			background: #FFFFFF;
			border-radius: 15upx;
			.tr{
				display: flex;
				align-items: center;
				text-align: center;
				justify-content: space-between;
				padding: 30upx;
				.td{
					position: relative;
					box-sizing: border-box;
					flex: 1;
					image{
						width: 46upx;
						height: 58upx;
					}
					text{
						display: block;
						font-size: 24upx;
						text-align: center;
						color: #999999;
					}
					&:after{
						content: "";
						width: 46upx;
						height: 7upx;
						background: url(../../static/image/icon_chain.png) repeat;
						background-size: 100%;
						position: absolute;
						right: -20%;
						top: 28%;
					}
					&:last-child:after{
						display: none;
					}
				}
			}
			.post{
				padding: 30upx;
				line-height: 24upx;
				text{
					font-size: 24upx;
					color: #999999;
					padding-right: 20upx;
					position: relative;
					border-right: 1px solid #e3e4e6;
					margin-left: 15upx;
					&:first-child{
						margin-left: 0;
					}
					&:last-child{
						border: none;
					}
					&.active{
						color: #0db983;
					}
				}
			}
			.alert{
				background: #f7f8fa;
				font-size: 24upx;
				color: #999999;
				line-height: 50upx;
				border-radius: 6upx;
				margin: 0 30upx;
				position: relative;
				padding-left: 50upx;
				&:before{
					content: "";
					width: 30upx;
					height:30upx;
					background: url(../../static/image/icon_tip_blue.png) repeat;
					background-size: 100%;
					position: absolute;
					left: 10upx;
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
			.headings{
				font-size: 28upx;
				color: #0db983;
				margin: 0 30upx;
				padding: 27upx 0;
			}
			.cn{
				font-size: 28upx;
				color: #555555;
				line-height: 47upx;
				margin: 0 30upx;
				text{
					display: block;
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
			.legend{
				width: 100%;
				margin-top: 20upx;
			}
		}
	}

	
	.section{
		background: #FFFFFF;
		border-radius: 15upx;
		margin: 20upx 30upx 0;
		.header{
			display: flex;
			align-items: center;
			justify-content: space-between;
			border-bottom: 1px solid #ebebeb;
			padding: 30upx;
			font-size: 32upx;
			.right{
				display: flex;
				align-items: center;
				color: #999999;
				image{
					width: 28upx;height: 30upx;margin-left: 15upx;
				}
			}
		}
		.body{
			padding: 30upx;
			font-size: 28upx;
			.colorBox{
				padding: 20upx;
				background: #f7f8fa;
				border-radius: 15upx;
			}
			.goods-item{
				display: flex;
				align-items: center;
				background: #fff;
				position: relative;
				overflow: hidden;
				border-radius: 10upx;
				.wrapper{
					flex: 1;
				}
				.u-box{
					font-size: 32upx;
					color: #333;
					display: flex;
					align-items: center;
					.name{
						margin-right: 30upx;
					}
				}
				.address-box{
					display: flex;
					align-items: center;
					margin-top: 16upx;
					.address{
						font-size: 24upx;
						color: #555;
					}
					.attr{
						font-size: 22upx;
						color: #555555;
						height: 32upx;
						line-height: 32upx;
						border-radius: 16upx;
						padding: 0 10upx;
						display: block;
						margin: 20upx 0;
						width: 100upx;
						text-overflow: ellipsis;
						white-space: nowrap;
						overflow: hidden;
						text-align: center;
						&.attr-blue{
							color: #2e8ae5;
							background-color: #eaf5ff;	
						}
						&.attr-red{
							color: #ff7f66;	
							background-color: #fdf1ec;	
						}
					}
				}
				.yticon{
					display: flex;
					align-items: center;
					height: 80upx;
					font-size: 40upx;
					color: #333;
					padding-left: 60upx;
				}
			}
			.submitway{
				.title{
					font-size: 28upx;
					padding-left: 20upx;
					position: relative;
					margin-bottom: 20upx;
					&:before{
						content: "";
						width: 1px;
						position: absolute;
						left: 0;
						height: 28upx;
						top: 50%;
						transform: translateY(-50%);
						background: #0DB983;
					}
				}
				.colorBox{
					margin-bottom: 30upx;
				}
				.zxType{
					.list{
						font-size: 28upx;
						color: #333333;
						display: flex;
						align-items: center;
						margin-bottom: 30upx;
						&:last-child{
							margin-bottom: 0;
						}
						image{
							width: 50upx;height: 50upx;margin-right: 20upx;
						}
					}
				}
				.yjType{
					.u-box{
						font-size: 32upx;
						color: #333;
						display: flex;
						align-items: center;
						image{
							width: 26upx;
							height: 32upx;
						}
						.name{
							margin-right: 30upx;
							margin-left: 20upx;
						}
						.tag{
							font-size: 22upx;
							color: #fff;
							background: #ff7f66;
							margin-left: 10upx;
							border-radius: 30upx;
							padding: 4upx 10upx;
							line-height: 1;
						}
					}
					.address-box{
						display: flex;
						align-items: center;
						margin-top: 16upx;
						.address{
							font-size: 24upx;
							color: #555;
						}
					}
				}
			}

		}
	}
	
	.users{
		.li{
			padding: 30upx 0;
			.add{
				margin-bottom: 40upx;
				position: relative;
			}
			.add,.minus{
				display: flex;
				align-items: center;
				justify-content: space-between;
				.left{
					display: flex;
					align-items: center;
					image{
						width: 32upx;height: 32upx;
						margin-right: 20upx;
					}
				}
				.right{
					.btn{
						font-size: 24upx;padding: 10upx 20upx;border: 1px solid #b3b3b3;border-radius: 30upx;color: #b3b3b3;
						margin-left: 20upx;position: relative;
						
					}
					.download:before{
							content: "";
							width: 16upx;
							height: 19upx;
							display: inline-block;
							margin-right: 10upx;
							background: url(../../static/image/icon_download_ss.png) no-repeat;
							background-size: 100%;
						}
					.zwBtn{
						color: #0db983;border-color: #0db983;
					}
					input{
						font-size: 24upx;
					}
				}
			}
		}
	}

	.defaultBox{
		padding: 30upx;
		padding-bottom: 200upx;
		text-align: center;
		image{
			width: 100%;
		}
		.msg{
			font-size: 28upx;color: #999999;margin-bottom: 40upx;
		}
		.btn{
			height: 85upx;
			line-height: 85upx;
			font-size: 32upx;
			color: #FFFFFF;
			background: #0DB983;
			text-align: center;
			border-radius: 42.5upx;
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
			.modal-lab{
				font-size: 28upx;color: #999999;text-align: center;line-height: 58upx;padding: 0 30upx;
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
				padding: 48upx 0;
				.item{
					display: flex;
					align-items: center;
					justify-content: space-between;
					font-size: 28upx;
					color: #333333;
					margin-bottom: 30upx;
					line-height: 100upx;
					height: 100upx;
					border: 1px solid #ebebeb;
					padding: 0 30upx;
					border-radius: 15upx;
					.right{
						font-size: 24upx;color: #555555;
					}
					&.active{
						background: #f6fcfa;border-color: #0db983;color: #0db983;
					}
					&.active .right{
						color: #52cc9d;
					}
					&:last-child{margin-bottom: 0;}
				}
			}
		}
	}
	.dateCalendar{
		padding: 0 !important;
		/deep/.uni-calendar__header{
			border: none !important;
			background: #f7f8fa;
		}
		/deep/.uni-calendar-item__weeks-box{
			position: relative;
		}
		/deep/.uni-calendar-item--isDay,
		/deep/.uni-calendar-item--checked{
			background: #0db983 !important;opacity: 1;color: #fff !important;
		}
		/deep/.uni-calendar-item--isDay-text{
			color: #0db983;
		}
		/deep/.uni-calendar__weeks:last-child{
			display: none !important;
		}
	}
</style>
