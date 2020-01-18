<template>
	<view class="content">
		<view class="phone">
			身份验证
		</view>
		<view class="title">
			请输入支付密码，以验证身份
		</view>
		<wakary-input type="box" :maxlength='6' @finish="finish"></wakary-input>
	</view>
</template>

<script>
	import wakaryInput from '@/components/wakary-input/wakary-input.vue'
	export default{
		components: {
			wakaryInput
		},
		data(){
			return{
				code:null
			}
		},
		methods:{
			navTo(url){
				uni.navigateTo({  
					url
				})  
			},
			finish(value){
				this.code = value
				if(this.code.length == 6){
					this.navTo('/pages/money/addBankcard')
				}
			}
		}
	}
</script>

<style lang="less">
	page{
		background: #f7f8fa;
	}
	.content{
		padding-top: 116upx;
		.title{
			font-size: 28upx;
			color: #999999;
			text-align: center;
			margin-top: 30upx;
			margin-bottom: 60upx;
		}
		.phone{
			font-size: 40upx;
			color: #000;
			text-align: center;
		}
		.btn {
		  border:1px solid rgb(13, 185, 131);
		  height: 84upx;
		  margin: 0 90upx;
		  text-align: center;
		  color: #0db983;
		  line-height: 84upx;
		  border-radius: 42upx;
		  font-size: 32upx;
		  margin-top: 60upx;
		}
	}
	
</style>
