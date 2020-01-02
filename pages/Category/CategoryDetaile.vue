<template>
	<view class="content">
		<uni-nav-bar class="navber" left-icon="back"  fixed backgroundColor="#0db983" color="#fff" :height="height" :top="top" @clickLeft="black">
			<view slot="left" v-if="visible">
				<view class="nav-item active" v-for="(item,index) in navs" :key="item" @click="Locateto(index)">
					{{item}}
				</view>
			</view>
			<!-- #ifndef MP -->
			<view slot="right" class="rightIcon">
				<image src="../../static/image/icon_collect2.png" mode=""></image>
				<image src="../../static/image/icon_service20.png" mode=""></image>
				<image src="../../static/image/icon_share20.png" mode=""></image>
			</view>
			<!-- #endif -->
		</uni-nav-bar>
		
		<scroll-view class="page-content" id="luTabStatic">
			<view class="tabbody" id="item0" >
				<image src="../../static/image/moneybg.png" mode="" class="bgImg"></image>
				<view class="flex-box">
					<view class="info">
						<view class="title">
							越南三个月多次认证
						</view>
						<view class="laber">
							<text>电子签</text><text>商务签</text>
						</view>
						<view class="foot">
							<view class="item">
								签送地：<text>西安</text>
							</view>
							<view class="item">
								办理时长：<text>10个工作日</text>
							</view>
						</view>
					</view>
					<view class="section">
						<view class="name">
							200
						</view>
						<view class="laber">
							<text>出签率 99%</text><text>办理人次 2589次</text>
						</view>
						<view class="ul">
							<view class="li">
								<view class="fte">
									3个月
								</view>
								<view class="data">
									有效期
								</view>
							</view>
							<view class="li">
								<view class="fte">
									7天
								</view>
								<view class="data">
									停留时间
								</view>
							</view>
							<view class="li">
								<view class="fte">
									多次
								</view>
								<view class="data">
									入境次数
								</view>
							</view>
						</view>
					</view>
				</view>
			</view>
			<view class="tabbody" id="item1" >
				<view class="card">
					<text class="card-header">办理流程</text>
					<view class="tr">
						<view class="td">
							<image src="../../static/image/icon_submit.png" mode="aspectFit"></image>
							<text>提交资料</text>
						</view>
						<view class="td">
							<image src="../../static/image/icon_upload.png" mode="aspectFit"></image>
							<text>传发资料</text>
						</view>
						<view class="td">
							<image src="../../static/image/icon_handle1.png" mode="aspectFit"></image>
							<text>办理</text>
						</view>
						<view class="td">
							<image src="../../static/image/icon_deliver.png" mode="aspectFit"></image>
							<text>配送</text>
						</view>
						<view class="td">
							<image src="../../static/image/icon_finish.png" mode="aspectFit"></image>
							<text>完成</text>
						</view>
					</view>
				</view>
			</view>
			<view class="tabbody" id="item2" >
				<view class="card">
					<view class="card-header">所需资料 <text class="all" @click="allshowClick">{{allshow?'全部关闭':'全部展开'}}</text></view>
					<view class="post">
						<text v-for="(item,index) in post" :key="index" :class="contentpage==index?'active':''">{{item}}</text>
					</view>
					<view class="alert">
						根据申请人身份类别，签证所需资料可能会有区别
					</view>
					<view class="collapse">
						<view class="panel" v-for="(item,index) in material" :key="index">
							<view class="collapse-header">
								<view class="left-aside">
									{{item.title}}
								</view>
								<view class="right-aside" @click="handleClickItem(item)">
									{{item.laber}}
									<image src="../../static/image/icon_down.png" mode="" :class="item.isShow?'show':''"></image>
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
						<view class="foot" @click="navTo('/pages/Category/CatematerialDetaile')">
							所有资料详情 <image src="../../static/image/icon_down.png" mode="" ></image>
						</view>
					</view>
				</view>	
			</view>
			<view class="tabbody" id="item3" >
				<view class="card">
					<view class="card-header">办理须知 </view>
					<view class="headings">
						受理范围
					</view>
					<view class="cn">
						<text>1.长期居住地或工作地在北京/天津/河北/河南/湖北/湖南/山西/内蒙古/西藏/甘肃/陕西/青海/宁夏/新疆的申请人(满足以上省市身份证/户口本/派出所证明原件/居住证/近6个月社保任一条件即可)。</text>
						<text>2.适用于：年收入10万左右，有一定经济能力的人士。</text>
					</view>
					<view class="headings">
						注意事项
					</view>
					<view class="cn">
						<text>1.1.不受理没有指定发达出境记录的外领区户口的申请者，和高危地区的申请人，如果寄资料，直接退回。</text>
						<text>(1) 指定发达国家:澳大利亚、英国、美国、加拿大、奧地利、比利时、智利、捷克、丹麦、芬兰、法国、德国、希腊、匈牙利、冰岛、爱尔兰、意大利、荷兰、新西兰、挪威、波兰、葡萄牙、西班牙、瑞典、瑞士</text>
						<text>(2) 高危地区:天津市(武清)、河北省、河南省、浙江省、福建省、黑龙江省、吉林省、辽宁省、山东省以及全国所有省市农村户口</text>
						<text>(注：天津、河北、河南地区申请人如有指定国家出境记录，也可受理。)</text>
						<text>2.敏感户籍/无发达国家出境记录可能会被要求提供学信网在线学籍报告。</text>
						<text>3.申请人的手机号码和在职电话要留意接听，需接受电话抽查，否则将延长办理时长!</text>
						<text>4.使领馆可能会致电单位电话或本人手机，请提交资料后注意接听，如有未接或不属实情况，可能会造成拒签。</text>
						<text>5.所有申请视个人资料情况,有可能会被退回或要求交押金，我司保留不受理的权利;如不受理，费用照退，请悉知。</text>
					</view>
					<view class="foot">
						所有资料详情 <image src="../../static/image/icon_down.png" mode="" ></image>
					</view>
				</view>	
				<view class="card">
					<view class="card-header">签证图例 </view>
					<image src="../../static/image/qztl.png" mode="aspectFit" class="legend"></image>
				</view>	
			</view>
		</scroll-view>
		<view class="flex-box-bottom">
			<view class="btn" >立即购买</view>
		</view>
	</view>
</template>

<script>
	import uniNavBar from "@/components/uni-nav-bar/uni-nav-bar.vue"
	import luBarTabNav from "@/components/lu-bar-tab-nav/lu-bar-tab-nav.vue";
	export default{
		components: {uniNavBar,luBarTabNav},
		data(){
			return{
				top:0,
				height:64,
				visible:false,
				scrollTop:0,
				navs:["商品","流程","资料","须知"],
				nodes:[],
				post:["在职人员","自由职业","退休人员","学生","学龄前儿童"],
				contentpage:0,
				material:[
					{title:'护照',content:'',laber:'原件',isShow:true},
					{title:'照片',content:'',laber:'原件',isShow:false},
					{title:'居住证',content:'',laber:'原件',isShow:false},
					{title:'结婚证',content:'',laber:'复印件',isShow:false},
					{title:'在职证明',content:'',laber:'原件',isShow:false},
					{title:'银行流水',content:'',laber:'复印件盖章',isShow:false},
					{title:'营业执照',content:'',laber:'复印件盖公章',isShow:false},
					{title:'辅助材料',content:'',laber:'原件',isShow:false}
				],
				allshow:false
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
		mounted() {
			this._queryMultipleNodes()
		},
		methods:{
			navTo(url){
				uni.navigateTo({  
					url
				})  
			}, 
			onPageScroll(e) {
				this.scrollTop = e.scrollTop
				if(this.scrollTop > 100){
					this.visible=true
				}else{
					this.visible=false
				}
			},
			black(){
				uni.navigateBack();
			},
			_queryMultipleNodes(){
				let list = new Array()
				for(let i=0;i<this.navs.length;i++){
					uni.createSelectorQuery().select("#item" + i).boundingClientRect().exec(res=>{
						if(res[0]){
							list.push(res[0].height)
						}
					})
				}
				this.nodes = list
			},
			Locateto(i){
				let scrollTop= 0
				this.nodes.slice(0,i).map((item,index)=>{
					scrollTop+=item
				})
				uni.pageScrollTo({
				    scrollTop: scrollTop-5,
				    duration: 100
				});
			},
			handleClickItem(i){
				this.material.map((item)=>{
					if(item.title == i.title){
						item.isShow =! item.isShow
					}
				})
			},
			allshowClick(){
				if(this.allshow){
					this.material.map((item)=>{
						item.isShow = false
					})
					this.allshow =false
				}else{
					this.material.map((item)=>{
						item.isShow = true
					})
					this.allshow =true
				}
			}
		}	
	}
</script>

<style lang="less" scoped>
	page{
		background: #f7f8fa;
	}
	.nav-item{
		float: left;
		font-size: 32upx;
		color: #b7e9d9;
		padding: 0 25upx;
		&:first-child{
			padding-left: 0;
		}
		&.active{
			color: #FFFFFF;
		}
	}
	.page-content{
		padding-bottom: 120upx;
	}
	.rightIcon{
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
		.bgImg{
			width: 100%;
			// position: absolute;
			// top: 0;
			// left: 0;
			height: 460upx;
		}
		.flex-box{
			margin: -430upx 30upx 0;
			position: relative;
			z-index: 10;
		}
		.info{
			.title{
				font-size: 45upx;
				color: #FFFFFF;
			}
			.laber{
				padding: 12upx 0 20upx;
				text{
					color: #FFFFFF;
					font-size: 24upx;
					padding: 6upx 20upx;
					background: #0ba373;
					border-radius: 20upx;
					margin-right: 20upx;
				}
			}
			.foot{
				font-size: 28upx;
				display: flex;
				justify-content: space-between;
				.item{
					flex: 1;
					color: #cdecdf;
					text{
						color: #FFFFFF;
					}
				}
			}
		}
		.section{
			background: #FFFFFF;
			padding: 30upx;
			border-radius: 15upx;
			margin-top: 30upx;
			.name{
				font-size: 36upx;
				color: #ff7f66;
				&:before{
					content: "￥";
					font-size: 28upx;
					color: #ff7f66;
					padding-right: 5upx;
				}
				&:after{
					content: "/人";
					font-size: 28upx;
					color: #999;
					padding-left: 5upx;
				}
			}
			.laber{
				padding: 12upx 0 20upx;
				text{
					color: #ff7f66;
					font-size: 24upx;
					padding: 6upx 20upx;
					background: #fdeee9;
					border-radius: 20upx;
					margin-right: 20upx;
				}
			}
			.ul{
				display: flex;
				align-items: center;
				justify-content: space-between;
				background: #FFFFFF;
				padding: 20upx 0;
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
						margin-top: 8upx;
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
		}
		.card{
			background: #FFFFFF;
			margin: 20upx 30upx;
			border-radius: 15upx;
			.card-header{
				height: 90upx;
				line-height: 90upx;
				padding: 0 28upx;
				font-size: 32upx;
				color: #000;
				position: relative;
				display: block;
				display: flex;
				align-items: center;
				justify-content: space-between;
				.all{
					font-size: 24upx;
					padding: 13upx 20upx;
					line-height: 28upx;
					border-radius: 30upx;
					color: #0db983;
					border: 1px solid #0db983;
				}
				&:after{
					content: "";
					position: absolute;
					bottom: 0;
					left: 0;
					right: 0;
					height: 1px;
					background: #f0f0f0;
				}
			}
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
	
	
	.flex-box-bottom{
		position: fixed;
		bottom: 0;
		left: 0;
		right: 0;
		padding: 10upx 45upx;
		background: #FFFFFF;
		z-index: 99;
		.btn{
			height: 84upx;
			line-height: 84upx;
			border-radius: 42upx;
			text-align: center;
			font-size: 32upx;
			width: 100%;
			background:#ff7f66;
			color: #fff;
		}
	}
	
</style>
