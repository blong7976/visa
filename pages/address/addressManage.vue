<template>
	<view class="content">
		<view class="row b-b">
			<text class="tit">收货人</text>
			<input class="input" type="text" v-model="addressData.name" placeholder="收货人姓名" placeholder-class="placeholder" />
		</view>
		<view class="row b-b">
			<text class="tit">手机号</text>
			<input class="input" type="number" v-model="addressData.mobile" placeholder="收货人手机号码" placeholder-class="placeholder" />
		</view>
		<view class="row b-b">
			<text class="tit">所在区域</text>
			<text @click="chooseLocation" class="input">
				{{addressData.addressName}}
			</text>
			<text class="yticon icon-shouhuodizhi"></text>
		</view>
		<view class="row b-b noborder"> 
			<text class="tit">详细地址</text>
			<input class="input" type="text" v-model="addressData.area" placeholder="楼号、门牌" placeholder-class="placeholder" />
		</view>
		
		<view class="row default-row">
			<text class="tit">设为默认</text>
			<switch :checked="addressData.defaule" color="#0db983" @change="switchChange" />
		</view>
		<button class="add-btn" @click="confirm">提交</button>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				addressData: {
					name: '',
					mobile: '',
					addressName: '在地图选择',
					address: '',
					area: '',
					default: false
				}
			}
		},
		onLoad(option){
			let title = '新增收货地址';
			if(option.type==='edit'){
				title = '编辑收货地址'
				
				this.addressData = JSON.parse(option.data)
			}
			this.manageType = option.type;
			uni.setNavigationBarTitle({
				title
			})
		},
		methods: {
			switchChange(e){
				this.addressData.default = e.detail;
			},
			
			//地图选择地址
			chooseLocation(){
				uni.chooseLocation({
					success: (data)=> {
						this.addressData.addressName = data.name;
						this.addressData.address = data.name;
					}
				})
			},
			
			//提交
			confirm(){
				let data = this.addressData;
				if(!data.name){
					uni.showToast({
						icon:'none',
						title:'请填写收货人姓名'
					})
					return;
				}
				if(!/(^1[3|4|5|7|8][0-9]{9}$)/.test(data.mobile)){
					uni.showToast({
						icon:'none',
						title:'请输入正确的手机号码'
					})
					return;
				}
				if(!data.address){
					uni.showToast({
						icon:'none',
						title:'请在地图选择所在位置'
					})
					return;
				}
				if(!data.area){
					uni.showToast({
						icon:'none',
						title:'请输入详细地址'
					})
					return;
				}
				setTimeout(()=>{
					uni.navigateBack()
				}, 800)
			},
		}
	}
</script>

<style lang="scss">
	page{
		background: #f7f8fa;
		padding-top: 16upx;
	}
	
	.row{
		display: flex;
		align-items: center;
		position: relative;
		padding:0 30upx;
		height: 110upx;
		background: #fff;
		&:before{
			content: "";
			position: absolute;
			left: 30upx;
			right: 30upx;
			bottom: 0;
			background: #ebebeb;
			height: 1px;
		}
		.tit{
			flex-shrink: 0;
			width: 140upx;
			font-size: 30upx;
			color: #333;
		}
		.input{
			flex: 1;
			font-size: 30upx;
			color: #333;
		}
		.icon-shouhuodizhi{
			font-size: 36upx;
			color: #333;
		}
	}
	.row:last-of-type:before{
		display: none;
	}
	.noborder:before{
		display: none;
	}
	.default-row{
		margin-top: 16upx;
		.tit{
			flex: 1;
		}
		switch{
			transform: translateX(16upx) scale(.9);
		}
	}
	.add-btn{
		display: flex;
		align-items: center;
		justify-content: center;
		width: 690upx;
		height: 80upx;
		margin: 60upx auto;
		font-size: 28upx;
		color: #fff;
		background-color: #0db983;
		border-radius: 10upx;
	}
</style>
