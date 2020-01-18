<template>
	<view class="content">
		<view class="alert">
			请填写开户银行
		</view>
		<view class="list-cell move">
			<view class="laber">银行</view>
			<view class="content" @click="navTo('/pages/money/bank')">
				<input type="text" v-model="phoneData.mobile" disabled placeholder-class="phClass" placeholder="请填写所属银行" />
			</view>
		</view>
		<view class="alert">
			请填写手机号
		</view>
		<view class="list-cell ">
			<view class="laber">手机号</view>
			<view class="content">
				<input type="text" v-model="phoneData.code" placeholder-class="phClass" placeholder="请输入银行预留手机号" />
			</view>
		</view>
		<view class="msg">
			信息加密处理，仅用于银行验证
		</view>
		<view class="m-nerror">
			<image src="../../static/image/icon_ridio_s_pre.png" mode="aspectFit" v-if="isagreement"   @click="isagreement=false"></image>
			<image src="../../static/icon_ridio_s.png" mode="aspectFit" v-else @click="isagreement=true"></image>
			同意
			<text style="color: #2e8ae5;" @click="navTo('/pages/money/agreement')">《用户协议》</text>
		</view>
		<view :class="isConfirm?'btn':'btn disabled'" @click="submit">
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
				isagreement:true,
				isConfirm:false
			}
		},
		watch: {
		  'phoneData.mobile': function(newVal){
			  if(newVal && this.phoneData.code && this.isagreement){
			  	this.isConfirm = true
			  }else{
			  	this.isConfirm = false
			  }
		   },
		  'phoneData.code': function(newVal){
			    if(newVal && this.phoneData.mobile && this.isagreement){
					this.isConfirm = true
			    }else{
					this.isConfirm = false
			    }
		  },
		  'isagreement': function(newVal){
		  		if(newVal && this.phoneData.mobile && this.phoneData.code){
		  			this.isConfirm = true
		  		}else{
		  			this.isConfirm = false
		  		}	  
		  }
		},
		onLoad(option){
			if(option.bank){
				this.phoneData.mobile = option.bank
			}
		},
		methods:{
			navTo(url){
				uni.navigateTo({
					url
				})
			},
			submit(){
				uni.showLoading({
					title:'请求中'
				})
				setTimeout(()=>{
					uni.hideLoading()
					this.navTo('/pages/money/addSuccess')
				}, 600);
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
	.msg{
		font-size: 28upx;
		color: #999;
		line-height: 70upx;
		padding-left: 180upx;
	}
	.move{padding-right: 60upx;}
	.move:after{
		content: " ";
		height: 11px;
		width: 11px;
		border-width: 2px 2px 0 0;
		border-color: #b3b3b3;
		border-style: solid;
		-webkit-transform: matrix(0.5, 0.5, -0.5, 0.5, 0, 0);
		transform: matrix(0.5, 0.5, -0.5, 0.5, 0, 0);
		position: absolute;
		top: 50%;
		margin-top: -7px;
		right: 30rpx;
	}
	.m-nerror{
		font-size: 28upx;color: #999999;
		padding: 0 90upx;
		margin-top: 60upx;
		image{
			width: 22upx;
			height: 22upx;
			background: #ebebeb;
			margin-right: 15upx;
		}
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
	  margin-top: 20upx;
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
