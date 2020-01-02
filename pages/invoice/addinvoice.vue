<template>
	<view class="content">
		<view class="row  move">
			<text class="tit">类型</text>
			<view class="content">
				<picker @change="bindPickerSexChange" :value="index" :range="sex">
					<view class="uni-input">{{sex[index]}}</view>
				</picker>
			</view>
		</view>
		<view :class="index==1?'row b-b noborder':'row b-b'">
			<text class="tit">抬头</text>
			<input class="input" type="text" v-model="info.name"  :placeholder="index==0?'公司名称':'个人姓名'" placeholder-class="placeholder" />
		</view>
		<view class="row b-b noborder" v-if="index==0"> 
			<text class="tit">税号</text>
			<input class="input" type="text" v-model="info.ein"  placeholder="纳税人识别字" placeholder-class="placeholder" />
		</view>
		
		<view class="row default-row noborder">
			<text class="tit">设为默认开票信息</text>
			<switch :checked="info.defaule" color="#0db983" @change="switchChange" />
		</view>
		<view class="flex-box-bottom">
			<view class="btn remove" v-if="isedit">删除</view>
			<view class="btn" @click="confirm">保存</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				info:{
					name: '',
					type: '',
					ein:'',
					defaule: false
				},
				sex:['企业','个人'],
				index: 0,
				isedit:false
			}
		},
		onLoad(option){
			let title = '新增我的发票';
			if(option.type==='edit'){
				title = '编辑我的发票'
				this.isedit = true
				this.info = JSON.parse(option.data)
				if(this.info.type === '个人'){
					this.index = 1
				}else{
					this.index = 0
				}
			}
			this.manageType = option.type;
			uni.setNavigationBarTitle({
				title
			})
		},
		methods: {
			switchChange(e){
				this.defaule = e.detail;
			},
			
			//提交
			confirm(){
				setTimeout(()=>{
					uni.navigateBack()
				}, 800)
			},
			bindPickerSexChange(e){
				this.index = e.target.value
			}
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
		font-size: 30upx;
		color: #333;
		&:before{
			content: "";
			position: absolute;
			left: 30upx;
			right: 30upx;
			bottom: 0;
			background: #ebebeb;
			height: 1px;
		}
		&:last-child:before{
			display: none;
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
	.b-b{
		.tit:after{
			content: "*";
			color: red;
			padding-left: 10upx;
		}
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
	.flex-box-bottom{
		position: fixed;
		bottom: 0;
		left: 0;
		right: 0;
		padding: 10upx 45upx;
		background: #FFFFFF;
		z-index: 99;
		display: flex;
		align-items: center;
		justify-content: space-between;
		.btn{
			height: 84upx;
			line-height: 84upx;
			border-radius: 42upx;
			text-align: center;
			font-size: 32upx;
			flex: 1;
			background:#0db983;
			color: #fff;
			margin-left: 30upx;
			display: flex;
			align-items: center;
			justify-content: center;
			&:first-child{
				margin-left: 0;
			}
		}
		.remove{
			background: #ff7f66;
			color: #FFFFFF;
		}
	}
</style>
