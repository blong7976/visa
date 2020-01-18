<template>
	<view class="content">
		<view class="alert">
			请绑定持卡人本人的银行卡
		</view>
		<view class="list-cell b-b">
			<view class="laber">持卡人</view>
			<view class="content">
				<input type="text" v-model="phoneData.mobile" placeholder-class="phClass" placeholder="请输入持卡人姓名"/>
			</view>
		</view>
		<view class="list-cell ">
			<view class="laber">卡号</view>
			<view class="content">
				<input type="text" v-model="phoneData.code" placeholder-class="phClass" placeholder="输入银行卡号"/>
			</view>
		</view>
		<view :class="isConfirm?'btn':'btn disabled'" @click="next">
			下一步
		</view>
	</view>
</template>

<script>
	export default {
		data(){
			return{
				phoneData: {
					mobile: '',
					code:''
				},
				isConfirm:false
			}
		},
		watch: {
		  'phoneData.mobile': function(newVal){
			  if(newVal && this.phoneData.code ){
			  	this.isConfirm = true
			  }else{
			  	this.isConfirm = false
			  }
		   },
		  'phoneData.code': function(newVal){
			    if(newVal && this.phoneData.mobile ){
					this.isConfirm = true
			    }else{
					this.isConfirm = false
			    }
		  }
		},
		methods:{
			navTo(url){
				uni.navigateTo({
					url
				})
			},
			next(){
				if(this.isConfirm){
					this.navTo('/pages/money/addBankcardNext');
				}
			}
		}
	}
</script>

<style lang="less">
	page{
		background: #f7f8fa;
	}
	.alert{
		padding: 20upx 30upx;
		font-size: 24upx;
		color: #999;
		line-height: 1.5;
		.icon{
			width: 28upx;
			height: 26upx;
			margin-right: 10upx;
			vertical-align: middle;
		}
	}
	.phClass{
		font-size: 28upx;
		color: #999;
	}
	.list-cell{
		position: relative;
		width: 100%;
		box-sizing: border-box;
		overflow: hidden;
		display: flex;
		align-items: center;
		justify-content: space-between;
		padding: 15px;
		font-size: 28upx;
		color: #333;
		background: #FFFFFF;
		padding-left: 150upx;
		.laber{
			position: absolute;
			left: 30upx;
		}
		.content {
			font-size: 28rpx;
			color: #666;
			line-height: 1;
			flex: 1;
			margin-left: 30upx;
			display: flex;
			align-items: center;
			justify-content: space-between;
			.getCode{
				font-size: 24upx;
				color: #999;
				padding: 15upx;
				border: 1px solid #999999;
				border-radius: 60upx;
				&.send{
					color: #333333;
					border-color: #333333;
				}
			}
		}
	}
	.mt20{
		margin-top: 20upx;
	}
	.b-b:before{
		content: "";
		height: 1px;
		left: 30upx;
		right: 30upx;
		position: absolute;
		bottom: 0;
		background: #ebebeb;
	}
	.btn {
	  background-color: rgb(13, 185, 131);
	  height: 84upx;
	  margin: 0 45upx;
	  margin-top: 60upx;
	  text-align: center;
	  color: #fff;
	  line-height: 84upx;
	  border-radius: 42upx;
	  font-size: 32upx;
	  &.disabled{
		  background: #ebebeb;
		  color: #999999;
	  }
	}
</style>
