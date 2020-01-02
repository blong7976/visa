<template>
	<view class="container">
		<!-- #ifdef MP -->
		<view class="mp-search-box">
			<input class="ser-input" type="text" value="搜索目的地" disabled />
		</view>
		<!-- #endif -->
		<!-- 头部背景 -->
		<view class="carousel-section">
			<view class="titleNview-background">
				<image src="../../static/image/IndexBanner1.png" style="width: 100%;height: 100%;" mode=""></image>
			</view>
		</view>
		
		<view class="cover-container">
			<!-- 热门签证 -->
<!-- 			<view class="f-header m-t">
				<image src="../../static/image/icon_hot.png"></image>
				<view class="tit-box">
					<text class="tit">热门签证</text>
				</view>
			</view> -->
			<view class="f-header m-t">
				<view class="tabs">
					<view v-for="(item,index) in countries" :key="item.name" :class="ispage==index?'tb active':'tb'" @click="handleCountries(index)">
						{{item.name}}
					</view>
				</view>
			</view>
			<view class="guess-section">
				<view 
					v-for="(item, index) in goodsList" :key="index"
					class="guess-item"
					@click="navToDetailPage(item)"
				>
					<view class="image-wrapper">
						<image :src="item.image" mode="aspectFill"></image>
					</view>
					<text class="title">{{item.title}}</text>
					<text class="price"><text class="span">￥</text>{{item.price}}<text class="span">起</text></text>
				</view>
			</view>
			<!-- <view class="ViewallBtn">查看全部</view> -->
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: '首页',
				ispage:0,
				countries:[
					{name:'欧洲'},{name:'澳洲'},{name:'美洲'},{name:'中东洲'},{name:'亚洲'},
				],
				/* 商品列表 */
				goodsList : [{
						image: "../../static/image/malaixiya.png",
						title: "中国",
						price: 179,
					},{
						image: "../../static/image/malaixiya.png",
						title: "美国",
						price: 179,
					},{
						image: "../../static/image/malaixiya.png",
						title: "德国",
						price: 179,
					},{
						image: "../../static/image/malaixiya.png",
						title: "马来西亚",
						price: 179,
					},{
						image: "../../static/image/malaixiya.png",
						title: "荷兰",
						price: 179,
					},{
						image: "../../static/image/malaixiya.png",
						title: "澳大利亚",
						price: 179,
					},{
						image: "../../static/image/malaixiya.png",
						title: "法国",
						price: 179,
					},{
						image: "../../static/image/malaixiya.png",
						title: "日本",
						price: 179,
					}
				]
				
			}
		},
		onLoad() {
			uni.setTabBarBadge({
			  index: 2,
			  text: '6'
			})
		},
		methods: {
			// #ifndef MP
			// 标题栏input搜索框点击
			onNavigationBarSearchInputClicked: async function(e) {
				
			},
			// #endif
			//详情
			navToDetailPage(item){
				let id = item.title;
				uni.navigateTo({
					url: `/pages/Category/Countries?id=${id}`
				})
			},
			handleCountries(index){
				this.ispage = index
			}
		}
	}
</script>

<style lang="less">
	/* #ifdef MP */
	.mp-search-box{
		position:absolute;
		left: 0;
		top: 30upx;
		z-index: 9999;
		width: 100%;
		padding: 0 40upx;
		box-sizing: border-box;
		-moz-box-sizing:border-box; /* Firefox */
		-webkit-box-sizing:border-box; /* Safari */
		.ser-input{
			flex:1;
			height: 60upx;
			line-height: 60upx;
			text-align: center;
			font-size: 28upx;
			color:#606266;
			border-radius: 20px;
			background: rgba(255,255,255,.8);
		}
	}
	/* #endif */
	page{
		.cate-section{
			position:relative;
			z-index:5;
			border-radius:16upx 16upx 0 0;
			margin-top:-20upx;
		}
		/* 头部 背景图 */
		.carousel-section {
			position: relative;
			padding-top: 10px;
			height: 500upx;
			.titleNview-background {
				position: absolute;
				top: 0;
				left: 0;
				width: 100%;
				height: 100%;
				transition: .4s;
			}
		}
	}
	.tabs{
		width: 100%;
		display: flex;
		align-items: center;
		justify-content: space-between;
		color: #999999;
		.tb{
			flex: 1;
			text-align: center;
			line-height: 88upx;
			font-size: 28upx;
			position: relative;
		}
		& .active{
			color: #000;
			font-weight: bold;
		}
		& .active:before{
			content: "";
			width: 50upx;
			height: 2px;
			background: #0db983;
			position: absolute;
			bottom: 10upx;
			left: 50%;
			transform: translateX(-50%);
		}
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
	.f-header{
		display:flex;
		align-items:center;
		height: 60upx;
		padding: 0 30upx 30upx;
		background: #fff;
		image{
			flex-shrink: 0;
			width: 32upx;
			height: 38upx;
			margin-right: 20upx;
		}
		.tit-box{
			flex: 1;
			display: flex;
			flex-direction: column;
		}
		.tit{
			font-size: 36upx;
			color: #333;
			line-height: 1.3;
			font-weight: 600;
		}
		.tit2{
			font-size: 24upx;
			color: #333333;
		}
		.icon-you{
			font-size: 24upx;
			color: #333333;
		}
	}
	.guess-section{
		display:flex;
		flex-wrap:wrap;
		padding: 0 30upx;
		background: #fff;
		.guess-item{
			display:flex;
			flex-direction: column;
			width: 48%;
			padding: 24upx;
			height: 140upx;
			padding-left: 170upx;
			position: relative;
			border: 1px solid #e6e6e6;
			box-sizing: border-box;
			border-radius: 8upx;
			margin-bottom: 24upx;
			&:nth-child(2n+1){
				margin-right: 4%;
			}
			&:nth-last-child(2),
			&:last-child{
				margin-bottom: 0;
			}
		}
		.image-wrapper{
			width: 133upx;
			height: 90upx;
			border: 1px solid #e6e6e6;
			box-sizing: border-box;
			overflow: hidden;
			position: absolute;
			left: 20upx;
			image{
				width: 100%;
				height: 100%;
				opacity: 1;
			}
		}
		.title{
			font-size: 32upx;
			color: #555;
			white-space: nowrap;
			text-overflow: ellipsis;
			overflow: hidden;
			margin-bottom: 18upx;
			font-weight: 600;
		}
		.price{
			font-size: 28upx;
			color: #ff7f66;
			line-height: 1;
			white-space: nowrap;
			text-overflow: ellipsis;
			overflow: hidden;
			.span:first-child{
				font-size: 20upx;
			}
			.span:last-child{
				font-size: 20upx;
				color: #999;
				padding-left: 6upx;
			}
		}
	}
	.ViewallBtn{
		width: 300upx;
		height: 60upx;
		line-height: 60upx;
		font-size: 24upx;
		text-align: center;
		margin: 40upx auto;
		border-radius: 30upx;
		color: #555555;
		background-color: #f0f0f0;
	}
</style>
