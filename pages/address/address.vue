<template>
	<view class="content b-t">
		<view class="list b-b" v-for="(item, index) in addressList" :key="index" @click="checkAddress(item)">
			<view class="wrapper">
				<view class="u-box">
					<text class="name">{{item.name}}</text>
					<text class="mobile">{{item.mobile}}</text>
					<text v-if="item.default" class="tag">默认</text>
				</view>
				<view class="address-box">
					<text class="address">{{item.addressName}} </text>
				</view>
			</view>
			<text class="yticon icon-bianji" @click.stop="addAddress('edit', item)"></text>
		</view>
		
		<button class="add-btn" @click="addAddress('add')">新增地址</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				source: 0,
				addressList: [
					{
						name: '刘晓晓',
						mobile: '18666666666',
						addressName: '广东省深圳市福田区皇岗街道办事处皇岗商务中心55楼滴加有限公司',
						address: '广东省深圳市福田区皇岗街道办事处皇岗商务中心55楼滴加有限公司',
						area: 'B区',
						default: true
					},{
						name: '易只咩',
						mobile: '15212345678',
						addressName: '陕西省西安市韩森寨街道 韩森路北侧新东尚(东区) 六号楼一单元1105室',
						address: '陕西省西安市韩森寨街道 韩森路北侧新东尚(东区) 六号楼一单元1105室',
						area: '西单元302',
						default: false,
					}
				]
			}
		},
		onLoad(option){
			console.log(option.source);
			this.source = option.source;
		},
		methods: {
			//选择地址
			checkAddress(item){
				if(this.source == 1){
					uni.navigateBack()
				}
			},
			addAddress(type, item){
				uni.navigateTo({
					url: `/pages/address/addressManage?type=${type}&data=${JSON.stringify(item)}`
				})
			},
			//添加或修改成功之后回调
			refreshList(data, type){
				//添加或修改后事件，这里直接在最前面添加了一条数据，实际应用中直接刷新地址列表即可
				this.addressList.unshift(data);
				
				console.log(data, type);
			}
		}
	}
</script>

<style lang='less'>
	page{
		padding-bottom: 120upx;
	}
	.content{
		position: relative;
	}
	.list{
		display: flex;
		align-items: center;
		padding: 30upx;;
		background: #fff;
		position: relative;
		&:before{
			content: "";
			position: absolute;
			left: 30upx;
			right: 30upx;
			bottom: 0;
			background: #ebebeb;
			height: 1px;
		}
	}
	.list:last-of-type:before{
		display: none;
	}
	.wrapper{
		display: flex;
		flex-direction: column;
		flex: 1;
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
	.u-box{
		font-size: 32upx;
		color: #333;
		display: flex;
		align-items: center;
		.name{
			margin-right: 30upx;
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
	.icon-bianji{
		display: flex;
		align-items: center;
		height: 80upx;
		font-size: 40upx;
		color: #333;
		padding-left: 60upx;
	}
	
	.add-btn{
		position: fixed;
		left: 30upx;
		right: 30upx;
		bottom: 16upx;
		z-index: 95;
		display: flex;
		align-items: center;
		justify-content: center;
		width: 690upx;
		height: 80upx;
		font-size: 32upx;
		color: #fff;
		background-color: #0db983;
		border-radius: 10upx;	
	}
</style>
