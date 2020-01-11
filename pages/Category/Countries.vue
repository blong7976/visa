<template>
	<view class="container">
		<uni-nav-bar class="navber" left-icon="back"  fixed backgroundColor="#0db983" color="#fff" :height="height" :top="top" @clickLeft="black">
			<view slot="left" v-if="visible">
				<view class="nav-item active">
					{{currentPageName}}
				</view>
			</view>
			<!-- #ifndef MP -->
			<view slot="right" class="rightIcon">
				<image src="../../static/image/icon_phone_s.png" mode=""></image>
				<image src="../../static/image/icon_service20.png" mode=""></image>
				<image src="../../static/image/icon_share20.png" mode=""></image>
			</view>
			<!-- #endif -->
		</uni-nav-bar>
		
		<!-- 头部背景 -->
		<view class="carousel-section">
			<view class="titleNview-background">
				<image src="../../static/image/bgimg_guojia.png" style="width: 100%;height: 100%;" mode=""></image>
			</view>
			<view class="state-info-box">
				<view class="state">
					<image src="../../static/image/malaixiya.png" mode=""></image>
					<text class="name">{{currentPageName}}</text>
				</view>
				<view class="statistical">
					已有21128人办理
				</view>
			</view>
		</view>
		
		<view class="cover-container">
			<view class="navbar">
				<view v-for="(item,index) in navList" :key="index" 
					 :class="currentPage===index?'nav-item current':'nav-item'"
					 @click="handleCurrentPage(index)">
					{{item}}
				</view>
			</view>
			<swiper @change="changeTab" :current="currentPage"  :style="{height:swiperHeight+'px'}">
				<swiper-item>
					<scroll-view>
						<view class="visatype swiper-body" >
							<view class="address" @tap="changeShow('QS_Picekr_custom_1')">
								<view class="lt">
									<image src="../../static/image/icon_location2.png" mode=""></image>
									常驻地
								</view>
								<view class="rt">
									{{HSBC}}
									<image src="../../static/image/icon_down.png" mode=""></image>
								</view>
							</view>
							<view class="navfilter">
								<view v-for="(item,index) in filterList" :key="index"
								     @click="handlefilter(index)"
								     :class="currentIndex==index?'filter-item currentfilter':'filter-item'">
									{{item}}
								</view>
							</view>
							<view class="visatypeList">
								<view v-for="(item,index) in visatypeList" :key="index" class="list-item" @click="navTo('/pages/Category/CategoryDetaile')">
									<view class="typeName">
										<view class="name">
											越南一个月单次旅游签证
										</view>
										<view class="price">
											<text class="value">
												<text class="em">¥</text>100
											</text>/人
										</view>
									</view>
									<text :class="item.level===1?'attr attr-blue':item.level===2?'attr attr-red':'attr attr-green'">
										{{item.level==1?'电子签':item.level==2?'贴纸签':'另纸签'}}
									</text>
									<view class="ul">
										<view class="li">
											<text>停留时间 </text>  7天
										</view>
										<view class="li">
											<text>办理时长 </text>  7天
										</view>
										<view class="li">
											<text>入境次数 </text>  2次
										</view>
										<view class="li">
											<text>办理人次 </text> 2650次
										</view>
									</view>
								</view>
							</view>
						</view>
					</scroll-view>
				</swiper-item>
				<swiper-item>
					<scroll-view >
						<view class="strategy swiper-body">
							<view class="p">
								1.我司为客户所提供的所有签证服务类别，均属于协助办理性质，您的美国旅游签证(全程1对1服务、陪同面签、录取指纹 | 快速审核资料直达领馆 )签证申请是否成功，完全由该国的签证官根据您递交的申请材料独立判断，本公司不得以任何方式的干预或交涉；并且在任何情况下，我司都不承担由签证申请结果而导致被追溯任何赔偿的责任和义务。
							</view>
							<view class="p">
								2.“预计工作日"为美国使馆签发签证时，正常情况下的处理时间；若遇特殊原因如假期、使馆内部人员调整、签证打印机故障等，则有可能会产生延迟出签的情况；对申请人根据签证预计日期提示，而进行的后续旅程安排所造成的可能经济损失，本公司不承担任何责任。
							</view>
							<view class="p">
								3.有关签证资料上公布的签证有效期和停留天数，仅做参考而非任何法定承诺，一切均以美国签证官签发的签证内容为唯一依据。
							</view>
							<view class="p">
								4.办理美国旅游签证(全程1对1服务、陪同面签、录取指纹 | 快速审核资料直达领馆 )签证申请者应在签证批准后再购买机票。凡因提前购买机票而签证未被批准所造成的经济损失，我社对此不负责任。
							</view>
							<view class="p">
								5.特别提示：签证结果返回我司后，您的护照及其它返回的原件资料，您可选择来我公司自取或委托快递寄送，如您选择快递寄送方式，则表示您授权我公司委托第三方进行快递服务，第三方公司（快递公司的）所有服务条款、权利与义务，您均已了解和认可。对于快递有可能带来的丢失、破损、或其他问题，由第三方公司（快递承运方)对您进行负责，我公司不予承担责任和由此产生的任何赔偿。当您选择我公司的产品或服务时，视同您已认同此条款的内容。
							</view>
						</view>
					</scroll-view>
				</swiper-item>
				<swiper-item>
					<scroll-view >
						<view class="consulting swiper-body">
							人工咨询
						</view>
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
		
		<QSpicker type="custom" ref="QS_Picekr_custom_1" pickerId="custom_1" :dataSet="customSet_1"
		 @confirm="confirm($event)" />
		
	</view>
</template>

<script>
	import uniNavBar from "@/components/uni-nav-bar/uni-nav-bar.vue"
	import luBarTabNav from "@/components/lu-bar-tab-nav/lu-bar-tab-nav.vue";
	import QSpicker from '@/components/QuShe-picker/QuShe-picker.vue';
	export default {
		components: {
			QSpicker,uniNavBar,luBarTabNav
		},
		data(){
			return {
				visible:false,
				currentPageName:''||'热门签证',
				height: 64, //header高度
				top: 0, //标题图标距离顶部距离
				scrollH: 0, //滚动总高度
				opcity: 0,
				iconOpcity: 0.5,
				navList:['签证类型','办证攻略','人工咨询'],
				currentPage:0,
				listHeight:0,  //内部的高度
				swiperHeight:0,  //外部的高度
				customSet_1: {},
				HSBC:'',//常驻地
				filterList:['全部','单次','多次','旅游','商务','探亲'],
				currentIndex:0,
				visatypeList:[{level:1},{level:2},{level:3},{level:1},{level:2},{level:1},{level:1},{level:3},{level:1},{level:1},{level:1}]
			}
		},
		async onLoad(options){
			// 	//接收传值,id里面放的是标题
			let id = options.id;
			this.currentPageName = id
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
		onShow() {
			let _this = this;
			setTimeout(function(){
				let list = ".visatype";
				_this.getlistHeight(list);
			},10) 
		},
		onPageScroll(e) {
			let scroll = e.scrollTop <= 0 ? 0 : e.scrollTop;
			let opcity = scroll / this.scrollH;
			if (this.opcity >= 1 && opcity >= 1) {
				return;
			}
			this.opcity = opcity;
			this.iconOpcity = 0.5 * (1 - opcity < 0 ? 0 : 1 - opcity)
		},
		onReady() {
			this.customSet_1 = {
				itemArray: [
					[{
						"name": "西安", //name变量名需与下方steps.steps_1_value相同
						"value": "西安" //可添加多项自定义想要的数据
					}, {
						"name": "北京",
						"value": "北京"
					}, {
						"name": "南京",
						"value": "南京"
					}]
				],
				defaultValue: [0, 0], //初始数据
				steps: {
					step_1_value: "name"
				}
			}
		},
		methods:{
			navTo(url){
				uni.navigateTo({  
					url
				})  
			},
			onPageScroll(e) {
				this.$nextTick(function(){
					this.scrollTop = e.scrollTop
					if(this.scrollTop > 100){
						this.visible=true
					}else{
						this.visible=false
					}
				})
			},
			black(){
				uni.navigateBack();
			},
			handleCurrentPage(index){
				this.currentPage = index
			},
			getlistHeight(list){
				let _this = this
				let info = uni.createSelectorQuery().select(list);
				info.boundingClientRect(function(data) {
					 _this.listHeight = data.height ; // 获取元素高度
					_this.getHeight();
				}).exec();
			},
			getHeight(){
				let _this = this;
				_this.swiperHeight = _this.listHeight;
				return _this.swiperHeight;
			},
			changeTab(e) { 
				let _this = this;
				this.currentPage = e.target.current
				// 不同的tab不同的高度赋不同的值
				if(e.target.current==0){
					let list = ".visatype";
					_this.getlistHeight(list);
				}else if(e.target.current==1){
					let list = ".strategy";
					_this.getlistHeight(list);
				}else if(e.target.current==2){
					let list = ".consulting";
					_this.getlistHeight(list);
				}
			},
			handlefilter(index){
				let self = this
				this.currentIndex = index
				uni.showLoading({
					title:'加载中',
					complete() {
						setTimeout(()=>{
							self.visatypeList = self.visatypeList.reverse()
							uni.hideLoading()
						},800)
					}
				})
			},
			changeShow(name) {
				this.$refs[name].show();
			},
			confirm(res) {
				this.HSBC = res.data[0].name
			}
		}
	}
</script>

<style lang="less">
	@import "../../static/icon.css";
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
	uni-page-wrapper{
		background-color: #fff;
	}
	.tui-header-box {
		width: 100%;
		position: fixed;
		left: 0;
		top: 0;
		z-index: 9998;
	}
	
	.tui-header {
		width: 100%;
		font-size: 18px;
		line-height: 18px;
		font-weight: 500;
		height: 32px;
		display: flex;
		align-items: center;
		justify-content: center;
	}
	
	.tui-header-icon {
		position: fixed;
		top: 0;
		left: 10px;
		display: flex;
		align-items: flex-start;
		justify-content: space-between;
		height: 32px;
		transform: translateZ(0);
		z-index: 99999;
	}
	.tui-icon {
		border-radius: 16px;
	}
	
	
	.tui-icon-back {
		height: 32px !important;
		width: 32px !important;
		display: block !important;
	}
	page{
		/* 头部 背景图 */
		.carousel-section {
			position: relative;
			padding: 32upx 50upx 0;
			height: 240upx;
			box-sizing: border-box;
			.titleNview-background {
				position: absolute;
				top: 0;
				left: 0;
				width: 100%;
				height: 100%;
				transition: .4s;
			}
			.state-info-box{
				position: relative;
				flex: 1;
				.state{
					margin-bottom: 20upx;
					image{
						width: 70upx;
						height: 50upx;
						border: 1px solid #fff;
						box-sizing: border-box;
						float: left;
						margin-right: 20upx;
					}
					.name{
						line-height: 50upx;
						font-size: 40upx;
						color: #fff;
						font-weight: bold;
					}
				}
			}
		}
	}
	.statistical{
		font-size: 24upx;
		color: #fff;
		height: 40upx;
		line-height: 40upx;
		background: rgba(0,0,0,.12);
		display: inline-block;
		padding: 0 20upx;
		border-radius: 20upx;
	}
	.cover-container{
		border-top-left-radius: 30upx;
		border-top-right-radius: 30upx;
		background: #FFFFFF;
		min-height: 100upx;
		position: relative;
		margin-top: -45upx;
		padding-top: 30upx;
	}
	.navbar{
		display: flex;
		height: 50upx;
		padding: 0 5px;
		justify-content: space-between;
		position: relative;
		z-index: 10;
		.nav-item{
			flex: 1;
			text-align: center;
			font-size: 28upx;
			color: #999;
			position: relative;
			&.current{
				color: #333333;
				font-weight: bold;
			}
			&.current:before{
				content: "";
				height: 2px;
				width: 40upx;
				background: #10ba84;
				position: absolute;
				left: 50%;
				transform: translateX(-50%);
				bottom: 0;
			}
		}
	}
	.swiper-body{
		padding: 30upx;
		box-sizing: border-box;
	}
	.address{
		width: 100%;
		height: 62upx;
		background: #f7f8fa;
		border-radius: 10upx;
		display: flex;
		justify-content: space-between;
		align-items: center;
		box-sizing: border-box;
		padding: 0 20upx;
		.lt{
			font-size: 24upx;
			color: #999999;
			image{
				width: 18upx;
				height: 22upx;
				margin-right: 10upx;
			}
		}
		.rt{
			font-size: 24upx;
			color: #333;
			image{
				width: 21upx;height: 11upx;margin-left: 10upx;position: relative;top: -4upx;
			}
		}
	}
	.navfilter{
		margin:30upx 0;
		overflow: hidden;
		.filter-item{
			font-size: 24upx;
			color: #999999;
			padding: 0 30upx;
			float: left;
			border-left: 1px solid #e3e4e6;
			&:first-child{
				padding-left: 0;border:none;
			}
			&.currentfilter{
				color: #0db983;
			}
		}
	}
	.visatypeList{
		overflow: hidden;
		.list-item{
			padding: 30upx;
			border: 1px solid #e0e0e0;
			border-radius: 10upx;
			margin-bottom: 30upx;
			&:last-child{
				margin-bottom: 0;
			}
		}
	}
	.typeName{
		display: flex;
		justify-content: space-between;
		overflow: hidden;
		align-items: center;
		.name{
			font-size: 32upx;
			color: #333333;
			max-width: 75%;
			text-overflow: ellipsis;
			white-space: nowrap;
			overflow: hidden;
		}
		.price{
			height: 50upx;
			line-height:50upx;
			font-size: 24upx;
			color: #999999;
			.value{
				font-size: 32upx;
				color: #ff7f66;
				.em{
					font-size: 22upx;
				}
			}
		}
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
		&.attr-green{
			color: #0db983;	
			background-color: #e6f8f2;	
		}
	}
	.ul{
		overflow: hidden;
		.li{
			width: 50%;
			float: left;
			font-size: 28upx;
			color: #555555;
			line-height: 40upx;
			text{
				color: #999999;
				margin-right: 20px;
			}
		}
	}
	.strategy{
		.p{
			font-size: 28upx;
			color: #555555;
			line-height: 45upx;
			margin-bottom: 20upx;
		}
	}
</style>
