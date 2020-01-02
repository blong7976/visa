<template>
	<view class="content">
		<view class="phone">
			设置密码
		</view>
		<view class="title">
			{{complete?'请再次填写确认':'请设置支付密码，用于支付验证'}}
		</view>
		<wakary-input type="box" :maxlength='6' @finish="finish"></wakary-input>
		<view class="btn" v-if="complete" @click="navTo('/pages/money/money')">
			完成
		</view>
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
				code:'',
				complete:false
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
					this.complete = true
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
		  background: #0db983;
		  color: #fff;
		  line-height: 84upx;
		  border-radius: 42upx;
		  font-size: 32upx;
		  margin-top: 60upx;
		}
	}
	
</style>
