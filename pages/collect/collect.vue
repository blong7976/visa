<template>
	<view class="content">
		<uni-nav-bar class="navber" left-icon="back" title="我的收藏"  fixed backgroundColor="#0db983" color="#fff" :height="height" :top="top" @clickLeft="black">
			<!-- #ifndef MP -->
			<view slot="right" class="rightIcon" @click="handle">
				{{edit?'完成':'管理'}}
			</view>
			<!-- #endif -->
		</uni-nav-bar>
		
		<view class="list">
			<view class="item" v-for="(item,index) in list" :key="item.id">
				<view class="edit" v-if="edit">
					<image
						:src="item.checked?'../../static/image/icon_checkbox_pre.png':'../../static/image/icon_checkbox.png'" 
						@click="check('item', index)"	
					mode="">
					</image>
				</view>
				<view class="flex-box">
					<view class="h1">
						<text class="name">日本一个月单次旅游签证</text>
						<text class="price">200</text>
					</view>
					<view class="attr attr-blue">电子签</view>
					<view class="h3">
						<text class="date">2019-12-29</text>
						<text class="btn">立即购买</text>
					</view>
				</view>
			</view>
		</view>
		
		<view class="tui-tabbar" v-if="edit">
			<view class="tui-flex-end">
				<image
					:src="allChecked?'../../static/image/icon_checkbox_pre.png':'../../static/image/icon_checkbox.png'" 
					@click="check"	
				mode="">
				全选
			</view>
			<view class="btn">
				<text>删除</text>
				<text class="attr-blue">分享</text>
			</view>
		</view>
	</view>
</template>

<script>
	import uniNavBar from "@/components/uni-nav-bar/uni-nav-bar.vue";
	import luBarTabNav from "@/components/lu-bar-tab-nav/lu-bar-tab-nav.vue";
	export default{
		components: {uniNavBar,luBarTabNav},
		data(){
			return{
				top:0,
				height:64,
				list: [{
					id: 1,
					attr_val: '电子签',
					level: 1,
					title: '丹麦一个月多次探亲签证',
					price: 100.00,
					number: 1,
					checked:false
				},
				{
					id: 3,
					attr_val: '贴纸签',
					level: 2,
					title: '美国一个月多次探亲签证',
					price: 200.00,
					number: 1,
					checked:false
				},{
					id: 4,
					attr_val: '贴纸签',
					level: 2,
					title: '日本一个月单次旅游签证',
					price: 300.00,
					number: 1,
					checked:false
				}],
				edit:false,
				allChecked:false,
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
			// #ifdef MP
			this.edit = true
			// #endif
		},
		methods:{
			navTo(url){
				uni.navigateTo({  
					url
				})  
			},
			black:function() {
				uni.navigateBack()
			},
			check(type, index){
				if(type === 'item'){
					this.list[index].checked = !this.list[index].checked;
				}else{
					const checked = !this.allChecked
					const list = this.list;
					list.forEach(item=>{
						item.checked = checked;
					})
					this.allChecked = checked;
				}
			},
			handle(){
				this.edit =! this.edit
			}
		}
	}
</script>

<style lang="less" >
	page{
		background: #f7f8fa;
		padding-bottom: 120upx;
	}
	.yticon{font-size: 24upx;}
	/deep/.uni-navbar__header-btns{
		flex: 1;
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
	
	.list{
		padding: 20upx 30upx;
		.item{
			background: #FFFFFF;
			border-radius: 20upx;
			padding: 36upx 30upx;
			margin-bottom: 20upx;
			display: flex;
			align-items: center;
			justify-content: space-between;
			.flex-box{flex: 1;}
			.edit{
				width: 45upx;
				height: 40upx;
				margin-right: 10upx;
				flex-shrink: 0;
				position:relative;
				font-size: 0;
				image{
					width: 32upx;
					height: 32upx;
					position:relative;
					top: 4upx;
					z-index: 5;
					vertical-align: middle;
				}
			}
			.h1{
				display: flex;
				align-items: center;
				justify-content: space-between;
				.name{
					font-size: 32upx;color: #333333;flex: 1;
				}
				.price{
					font-size: 32upx;color: #ff7f66;
					&:before{
						content: "￥";
						font-size: 24upx;
					}
					&:after{
						content: "/人";
						font-size: 24upx;
						color: #999;
					}
				}
			}
			.h3{
				display: flex;
				align-items: center;
				justify-content: space-between;
				.date{
					font-size: 28upx;color: #999999;
				}
				.btn{
					font-size: 28upx;
					color: #0DB983;
					height: 60upx;
					line-height: 60upx;
					width: 160upx;
					text-align: center;
					border-radius: 30upx;
					border: 1px solid #0DB983;
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
	}
	
	.tui-tabbar{
		background: #FFFFFF;
		height: 100upx;
		display: flex;
		align-items: center;
		justify-content: space-between;
		position: fixed;
		bottom: 0;
		left: 0;
		right: 0;
		box-sizing: border-box;
		padding: 0 30upx;
		.tui-flex-end{
			font-size: 28upx;
			color: #999999;
			display: flex;
			align-items: center;
			justify-content: flex-start;
			text{
				font-size: 34upx;
				color: #ff7f66;
				font-weight: 600;
				&:before{
					content: "￥";
					font-size: 28upx;
					font-weight: 400;
					margin-left: 10upx;
				}
			}
			image{
				width: 32upx;
				height: 32upx;
				position:relative;
				top: 4upx;
				z-index: 5;
				vertical-align: middle;
				margin-right: 10upx;
			}
		}
		.btn{
			text{
				height: 72upx;
				line-height: 72upx;
				width: 160upx;
				text-align: center;
				border-radius: 36upx;
				font-size: 28upx;
				color: #555;
				border:1px solid #b3b3b3;
				display: block;
				float: left;
				margin-right: 20upx;
				&:last-child{
					margin-right: 0;
				}
				&.attr-blue{
					color: #0db983;
					border-color: #0db983;	
				}
			}
			
		}
	}
</style>
