<template>
	<view class="container">
		<view class="title">
			一.【本服务】
		</view>
		<view class="box">
			<view class="p">
				1.1微信支付服务，指本公司依托微信及微信公众平台为收付款人之间提供的货币资金转移服务。(下称“本服务")
			</view>
			<view class="p">
				1.2本服务包括余额支付和快捷支付两种类型。
			</view>
			<view class="p">
				1.2.1余额支付，指你使用本公司给你开立的支付账户中.的余额进行资金转移的一-种支付方式。你确认并同意本公司给你开立支付账户时，将你的微信号与该支付账户相关联，使得你可以通过微信的“零钱"功能使用该支付账户(以下所称的“零钱”即指该支付账户，也等同于《财付通，服务协议》中所指的财付通账户)。你有权使用“零钱”中的余额进行消费和转账，若余额不足，你需先开通快捷支付，并向”零钱'充值，你也可以通过接收他人的转账来增加“零钱”的余额。
			</view>
		</view>
		
		<view class="title">
			二、【账户和信息安全】
		</view>
		<view class="box">
			<view class="p">
				2.1你应自行设置微信号的登录密码和微信支付密码，并予以妥善保管。你的微信号将与本公司给你配置的支付账户关联，不能单独使用，若你的微信号注销，则与其关联的支付账户也随之注销，使得你无法通过该微信号使用本服务。为满足法律法规的要求以及使用本服务的核心功能，你需提交你的姓名、身份证号、手机号、银行卡信息等信息。你授权本公司在法律规定的范围内保存你的姓名、身份证号、手机号、银行卡号、交易订单、交易记录等信息，以供向你持续性地提供和推广优质服务。你同意:
			</view>
			<view class="p">
				2.1.1你应按照本公司要求提供并及时更新你的信息，若你提供的信息错误、不实、过期或不完整，本公司有权暂停或终止向你提供部分或全部服务。
			</view>
		</view>
		
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		methods:{
			
		}
	}
</script>

<style lang='less'>
	page{
		background: #FFFFFF;
		padding:0 30upx;
		.title{
			margin-top: 20upx;
			margin-bottom: 28upx;
			font-size: 24upx;
			color: #333;
			font-weight: bold;
			margin-top: 30upx;
		}
		.p{
			font-size: 28upx;
			color: #555;
			line-height: 44upx;
			margin-bottom: 20upx;
		}
	}
</style>
