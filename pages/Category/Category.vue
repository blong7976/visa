<template>
	<view class="container">
		<!-- #ifdef MP -->
		<view class="mp-search-box">
			<input class="ser-input" type="text" value="搜索目的地" disabled @click="handleCategoryList" />
		</view>
		<!-- #endif -->
		<view class="content">
			<scroll-view scroll-y class="left-aside">
				<view v-for="item in flist" :key="item.id" class="f-item b-b" :class="{active: item.id === currentId}" @click="tabtap(item)">
					{{item.name}}
				</view>
			</scroll-view>
			<scroll-view scroll-with-animation scroll-y class="right-aside" @scroll="asideScroll" :scroll-top="tabScrollTop">
				<view class="s-list">
					<text class="s-item">{{currentName}}</text>
					<view class="t-list">
						<view class="t-item" v-for="titem in tlist" :key="titem.id" @click="navToList(titem)" >
							<text>{{titem.name}}</text>
						</view>
					</view>
				</view>
			</scroll-view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: '分类',
				sizeCalcState: false,
				tabScrollTop: 0,
				currentId: 1,
				currentName:null,
				flist: [],//一级分类
				slist: [],//内容仓库
				tlist: [],//要显示的列表
				cateList: [
					{
						id: 1,
						name: '热门签证'
					},
					{
						id: 2,
						name: '欧洲'
					},
					{
						id: 3,
						name: '澳洲'
					},
					{
						id: 4,
						name: '美洲'
					},
					{
						id: 5,
						pid: 1,
						name: '迪拜'
					},
					{
						id: 6,
						pid: 1,
						name: '沙特阿拉伯'
					},
					{
						id: 8,
						pid: 1,
						name: '刚果金',
					},
					{
						id: 9,
						pid: 1,
						name: '埃及',
					},
					{
						id: 10,
						pid: 1,
						name: '肯尼亚',
					},
					{
						id: 11,
						pid: 1,
						name: '南非',
					},
					{
						id: 12,
						pid: 1,
						name: '埃塞俄比亚',
					},
					{
						id: 14,
						pid: 1,
						name: '喀麦隆',
					},
					{
						id: 15,
						pid: 1,
						name: '卢旺达',
					},
					{
						id: 16,
						pid: 2,
						name: '芬兰',
					},
					{
						id: 17,
						pid: 2,
						name: '瑞典',
					},
					{
						id: 18,
						pid: 2,
						name: '英国',
					},{
						id: 19,
						pid: 3,
						name: '澳大利亚',
					},{
						id: 20,
						pid: 3,
						name: '新西兰',
					},{
						id: 21,
						pid: 3,
						name: '图瓦卢',
					},{
						id: 22,
						pid: 4,
						name: '玻利维亚',
					},{
						id: 23,
						pid: 4,
						name: '美国',
					},{
						id: 24,
						pid: 4,
						name: '阿根廷',
					}
				]
			}
		},
		onLoad() {
			this.loadData();
		},
		methods: {
			loadData(){
				let list = this.cateList;
				list.forEach(item=>{
					if(!item.pid){
						this.flist.push(item);  //pid为父级id, 没有pid是一级分类
					}else{
						this.slist.push(item); //内容仓库
					}
				})
				this.currentName =  this.flist[0].name
				this.tlist = this.slist.filter(sitem=>sitem.pid === this.flist[0].id) 
			},
			//一级分类点击
			tabtap(item){
				this.currentId = item.id;
				this.currentName =  item.name;
				this.tlist = this.slist.filter(sitem=>sitem.pid === item.id)
			},
			//详情
			navToList(item){
				let id = item.name;
				uni.navigateTo({
					url: `/pages/Category/Countries?id=${id}`
				})
			},
			handleCategoryList(){
				uni.navigateTo({
					url:'/pages/Category/Categorylist'
				})
			},
			onNavigationBarSearchInputClicked: async function(e) {
				uni.navigateTo({
					url:'/pages/Category/Categorylist'
				})
			},
		}
	}
</script>

<style lang='less'>
	/* #ifdef MP */
	.mp-search-box{
		position:absolute;
		left: 0;
		top: 10upx;
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
			border: 1px solid #ddd;
		}
	}
	.content {
		display: flex;
		padding-top: 80upx;
		box-sizing: border-box;
	}
	/* #endif */
	
	page,
	.container,
	.content {
		height: 100%;
		background-color: #FFFFFF;
	}
	.container{background-color: #007AFF;}
	.content {
		display: flex;
	}
	.left-aside {
		flex-shrink: 0;
		width: 200upx;
		height: 100%;
		background-color: #fff;
	}
	.f-item {
		display: flex;
		align-items: center;
		justify-content: center;
		width: 100%;
		height: 100upx;
		font-size: 24upx;
		color: #303133;
		position: relative;
		&.active{
			color: #0db983;
			background: #f8f8f8;
			font-size: 28upx;
			font-weight: 600;
		}
	}

	.right-aside{
		flex: 1;
		overflow: hidden;
		padding-left: 20upx;
		background-color: #f8f8f8;
	}
	.s-item{
		display: flex;
		align-items: center;
		height: 70upx;
		padding-top: 8upx;
		font-size: 28upx;
		color: #303133;
	}
	.t-list{
		display: flex;
		flex-wrap: wrap;
		width: 100%;
		&:after{
			content: '';
			flex: 99;
			height: 0;
		}
	}
	.t-item{
		flex-shrink: 0;
		display: flex;
		justify-content: center;
		align-items: center;
		flex-direction: column;
		width: 176upx;
		font-size: 24upx;
		color: #555;
		background: #fff;
		width: 148upx;
		height: 58upx;
		line-height: 60upx;
		border-radius: 6px;
		border-width: 1px;
		border-color: rgb(230, 230, 230);
		border-style: solid;
		margin-right: 20upx;
		margin-bottom: 20upx;
		text-overflow: ellipsis;
		white-space: nowrap;
		overflow: hidden;
		&:nth-child(3n){
			margin-right: 0;
		}
	}

</style>
