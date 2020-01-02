<template>
	<view class="container">
		<view class="list-cell b-b " @click="navTo('/pages/about/about')" hover-class="cell-hover" :hover-stay-time="50">
			<text class="cell-tit">关于我们</text>
			<text class="cell-more yticon icon-you"></text>
		</view>
		<view class="list-cell b-b" hover-class="cell-hover" :hover-stay-time="50">
			<text class="cell-tit">给个好评</text>
			<text class="cell-more yticon icon-you"></text>
		</view>
		<view class="list-cell" @click="clickversion">
			<text class="cell-tit">检查更新</text>
			<text class="cell-tip">Version 1.0.1</text>
			<text class="cell-more yticon icon-you"></text>
		</view>
		<view class="list-cell m-t" @click="navTo('/pages/set/writeCode')">
			<text class="cell-tit">设置密码</text>
			<text class="cell-more yticon icon-you"></text>
		</view>
		<view class="list-cell log-out-btn" @click="toLogout">
			<text class="cell-tit">退出登录</text>
		</view>
		
		<!-- 更新弹窗 -->
		<view class="modal" v-if="newVersion">
			<view class="modal-body">
				<image src="../../static/image/bbgxbg.png" mode=""></image>
				<text class="Version">V1.0.2</text>
				<view class="content">
					<text class="msg">1.解决了一些已知问题 </text>
					<text class="msg">2.优化签证申请提交流程，办签更高效，流程更清晰</text>
				</view>
				<view class="btn">
					立即更新
				</view>
				<view class="btn nobg">
					残忍拒绝
				</view>
				<view class="close" @click="closeModal">
					<image src="../../static/image/icon_close_w.png" mode=""></image>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				newVersion:false
			};
		},
		methods:{
			navTo(url){
				uni.navigateTo({
					url
				})
			},
			//退出登录
			toLogout(){
				uni.showModal({
				    content: '确定要退出登录么',
				    success: (e)=>{
				    	if(e.confirm){
				    		setTimeout(()=>{
				    			uni.navigateTo({
				    				url:'/pages/login/loginCode'
				    			})
				    		}, 200)
				    	}
				    }
				});
			},
			clickversion(){
				uni.showLoading({
					title:'检测中'
				})
				setTimeout(() => {
					uni.hideLoading()
					this.newVersion = true
				}, 600);
			},
			closeModal(){
				this.newVersion = false
			}
		}
	}
</script>

<style lang='less'>
	page{
		background: #f7f8fa;
	}
	.list-cell{
		display:flex;
		align-items:baseline;
		padding: 20upx 30upx;
		line-height:60upx;
		position:relative;
		background: #fff;
		justify-content: center;
		&.log-out-btn{
			margin: 40upx 30upx;
			border: 1px solid #ff7f66;
			border-radius: 50upx;
			padding: 0;
			line-height: 84upx;
			background: #f7f8fa;
			.cell-tit{
				color: #ff7f66;
				font-size: 32upx;
				text-align: center;
			}
		}
		&.cell-hover{
			background:#fafafa;
		}
		&.b-b:after{
			left: 30upx;
			content: "";
			height: 1px;
			right: 30upx;
			background: #ebebeb;
			position: absolute;
			bottom: 0;
		}
		&.m-t{
			margin-top: 16upx; 
		}
		.cell-more{
			align-self: baseline;
			font-size:28upx;
			color:#666;
			margin-left:10upx;
		}
		.cell-tit{
			flex: 1;
			font-size: 28upx;
			color: #333;
			margin-right:10upx;
		}
		.cell-tip{
			font-size: 28upx;
			color: #b3b3b3;
		}
	}
	
	.modal{
		position: fixed;
		top:0;
		left:0;
		bottom:0;
		right: 0;
		background: rgba(0,0,0,.5);
		z-index: 999;
		.modal-body{
			position: fixed;
			left: 50%;
			top: 50%;
			margin: auto;
			background: #fff;
			z-index: 9999;
			transition: all 0.3s ease-in-out;
			box-sizing: border-box;
			transform: translate(-50%, -50%) scale(1);
			width: 560upx;
			padding-bottom: 10upx;
			border-radius: 10px;
			image{
				width: 100%;
				height: 242upx;
				border-top-left-radius: 10px;
				border-top-right-radius: 10px;
			}
			.Version{
				position: absolute;
				top: 130upx;
				left:50%;
				transform: translateX(-50%);
				font-size: 28upx;
				color: #fff;
				background-color: #ffc44c;
				text-align: center;
				height: 40upx;
				padding:0 20upx;
				display: flex;
				align-items: center;
				justify-content: center;
				border-radius: 20upx;
			}
			.close{
				width: 30upx;
				height: 30upx;
				position: absolute;
				bottom: -70upx;
				left: 50%;
				transform: translateX(-50%);
				image{
					width: 100%;height: 100%;
				}
			}
			.content{
				width: 100%;
				padding: 30upx;
				box-sizing: border-box;
				text{
					display: block;
				}
				.msg{
					font-size: 28upx;
					color: #333;
					line-height: 1.5;
					margin-bottom: 15upx;
				}
			}
			.btn {
			  background-color: #0db983;
			  width: 380upx;
			  height: 72upx;
			  text-align: center;
			  line-height: 72upx;
			  border-radius: 36upx;
			  margin: 0 auto;
			  margin-top: 0upx;
			  color: #FFFFFF;
			  font-size: 32upx;
			  box-shadow: 0 1px 22px 0 rgb(180, 220, 208), 0 4px 8px 0 rgb(237, 241, 240);
			}
			.nobg{
				background: transparent;
				color:#999;
				font-size: 28upx;
				margin-top: 4px;
				box-shadow: none;
			}
		}
	}
</style>
