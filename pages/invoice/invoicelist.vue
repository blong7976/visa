<template>
	<view class="content b-t">
		<view class="list b-b" v-for="(item, index) in addressList" :key="index" @click="checkAddress(item)">
			<view class="wrapper">
				<view class="u-box">
					<text class="name">{{item.name}}</text>
					<text v-if="item.defaule" class="tag">默认</text>
				</view>
				<view class="address-box">
					<text class="address">类型：{{item.type}} </text>
				</view>
			</view>
			<text class="yticon icon-bianji" @click.stop="addAddress('edit', item)"></text>
		</view>
		
		<button class="add-btn" @click="addAddress('add')">+ 新增发票</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				source: 0,
				addressList: [
					{
						name: '刘德华',
						type: '个人',
						defaule: true
					},{
						name: '重庆优恳设计公司',
						type: '企业',
						ein:'6123284798522',
						defaule: false
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
					url: `/pages/invoice/addinvoice?type=${type}&data=${JSON.stringify(item)}`
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
