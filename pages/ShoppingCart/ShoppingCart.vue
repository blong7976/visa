<template>
	<view class="container">
		<!-- 空白页 -->
		<view v-if="empty===true" class="empty">
			<view class="empty-tips">
				空空如也
			</view>
		</view>
		<view v-else>
			<!-- 列表 -->
			<view class="cart-list">
				<block v-for="(item, index) in cartList" :key="item.id">
					<view
						class="cart-item" 
						:class="{'b-b': index!==cartList.length-1}"
					>
						<view class="image-wrapper">
							<image 
								:src="item.checked?'../../static/image/icon_checkbox_pre.png':'../../static/image/icon_checkbox.png'" 
								@click="check('item', index)"	
							mode="">
							</image>
						</view>
						<view class="item-right">
							<text class="clamp title">{{item.title}}</text>
							<text :class="item.level===1?'attr attr-blue':'attr attr-red'">{{item.attr_val}}</text>
							<view class="price">
								<text class="value">
									<text class="em">¥</text>{{item.price}}
								</text>/人
							</view>
							<uni-number-box
								class="step"
								:min="1" 
								:value="item.number"
								:isMin="item.number===1"
								:index="index"
								:disabled="true"
								@eventChange="numberChange"
							></uni-number-box>
						</view>
					</view>
				</block>
			</view>
			<!-- 底部菜单栏 -->
			<view class="action-section">
				<view class="checkbox" >
					<image 
						:src="allChecked?'../../static/image/icon_checkbox_pre.png':'../../static/image/icon_checkbox.png'" 
						mode="aspectFit"
						class="icon"
						@click="check('all')"
					></image>
					<view class="clear-btn" @click="check('all')">
						全选
					</view>
					<!-- #ifdef MP -->
					<text class="editBtn" v-if="!isEdit" @click="isEdit=true">管理</text>
					<!-- #endif -->
				</view>
				
				
				<block v-if="!isEdit">
					<view class="total-box">
						<text class="price">合计<text>¥{{total}}</text></text>
					</view>
					<button type="primary" class="no-border confirm-btn" @click="createOrder">结算</button>
				</block>
				
				<view class="editbox" v-else>
					<button type="default" plain="true" class="no-border confirm-btn btnok" @click="isEdit=false">完成</button>
					<button type="primary" class="no-border confirm-btn collect-btn" @click="goodCollect">移入我的收藏</button>
					<button type="primary" class="no-border confirm-btn del-btn" @click="goodDetail">删除</button>
				</view>
				
			</view>
		</view>
	</view>
</template>

<script>
	import uniNumberBox from '@/components/uni-number-box.vue'
	export default {
		components:{
			uniNumberBox
		},
		data() {
			return {
				isEdit:false,//管理 true|false
				total: 0, //总价格
				allChecked: false, //全选状态  true|false
				empty: false, //空白页现实  true|false
				cartList: [{
					id: 1,
					attr_val: '电子签',
					level: 1,
					title: '丹麦一个月多次探亲签证',
					price: 100.00,
					number: 1,
					checked:false
				},
				{
					id: 3,
					attr_val: '贴纸签',
					level: 2,
					title: '美国一个月多次探亲签证',
					price: 200.00,
					number: 1,
					checked:false
				},{
					id: 4,
					attr_val: '贴纸签',
					level: 2,
					title: '日本一个月单次旅游签证',
					price: 300.00,
					number: 1,
					checked:false
				}],
			};
		},
		onLoad(){
		},
		watch:{
		},
		methods: {
			//数量
			numberChange(data){
				this.cartList[data.index].number = data.number;
				this.calcTotal();
			},
			//选中状态处理
			check(type, index){
				if(type === 'item'){
					this.cartList[index].checked = !this.cartList[index].checked;
				}else{
					const checked = !this.allChecked
					const list = this.cartList;
					list.forEach(item=>{
						item.checked = checked;
					})
					this.allChecked = checked;
				}
				this.calcTotal(type);
			},
			//计算总价
			calcTotal(){
				let list = this.cartList;
				if(list.length === 0){
					this.empty = true;
					return;
				}
				let total = 0;
				let checked = true;
				list.forEach(item=>{
					if(item.checked === true){
						total += item.price * item.number;
					}else if(checked === true){
						checked = false;
					}
				})
				this.allChecked = checked;
				this.total = Number(total.toFixed(2));
			},
			//创建订单
			createOrder(){
				let list = this.cartList;
				let goodsData = [];
				list.forEach(item=>{
					if(item.checked){
						goodsData.push({
							id: item.id,
							attr_val: item.attr_val,
							number: item.number
						})
					}
				})
				uni.navigateTo({
					url:'/pages/ShoppingCart/createOrder'
				})
			},
			
			// 管理按钮
			onNavigationBarButtonTap(e) {
				const index = e.index;
				if (index === 0) {
					this.isEdit = true
					// #ifdef APP-PLUS
					const pages = getCurrentPages();
					const page = pages[pages.length - 1];
					const currentWebview = page.$getAppWebview();
					currentWebview.setTitleNViewButtonStyle(0, {  
					    text: '完成',  
					}); 
					// #endif
				}
			},
			// 加入收藏
			goodCollect(){
				let list = this.cartList.filter(item => item.checked);
				if(list.length<=0){
					uni.showModal({
					    title: '提示',
					    content: '您还没有选择宝贝哦！',
					    success: function (res) {
					        if (res.confirm) {
					            console.log('用户点击确定');
					        } else if (res.cancel) {
					            console.log('用户点击取消');
					        }
					    }
					});
				}else{
					uni.showToast({
						icon:'success',
						title:'加入成功'
					})
				}
			},
			// 删除
			goodDetail(){
				let list = this.cartList.filter(item => item.checked);
				if(list.length<=0){
					uni.showModal({
					    title: '提示',
					    content: '您还没有选择宝贝哦！',
					    success: function (res) {
					        if (res.confirm) {
					            console.log('用户点击确定');
					        } else if (res.cancel) {
					            console.log('用户点击取消');
					        }
					    }
					});
				}else{
					uni.showToast({
						icon:'success',
						title:'删除成功'
					})
				}
			}
		}
	}
</script>

<style lang='less'>
	page{
		background-color: #f7f8fa;
	}
	.container{
		padding-bottom: 134upx;
		/* 空白页 */
		.empty{
			position:fixed;
			left: 0;
			top:0;
			width: 100%;
			height: 100vh;
			padding-bottom:100upx;
			display:flex;
			justify-content: center;
			flex-direction: column;
			align-items:center;
			background: #fff;
			image{
				width: 240upx;
				height: 160upx;
				margin-bottom:30upx;
			}
			.empty-tips{
				display:flex;
				font-size: 28upx;
				color: #555555;
				.navigator{
					color:#555555;
					margin-left: 16upx;
				}
			}
		}
	}
	/* 购物车列表项 */
	.cart-item{
		display:flex;
		position:relative;
		padding:20upx;
		margin: 30upx;
		background: #FFFFFF;
		border-radius: 20upx;
		.image-wrapper{
			width: 45upx;
			height: 40upx;
			flex-shrink: 0;
			position:relative;
			font-size: 0;
			image{
				width: 32upx;
				height: 32upx;
				position:relative;
				top: 4upx;
				z-index: 5;
				vertical-align: middle;
			}
		}
		.checkbox{
			position:absolute;
			left:-16upx;
			top: -16upx;
			z-index: 8;
			font-size: 44upx;
			line-height: 1;
			padding: 4upx;
			color: #555555;
			background:#fff;
			border-radius: 50px;
			.icon{
				width: 32upx;
				height: 32upx;
			}
		}
		.item-right{
			display:flex;
			flex-direction: column;
			flex: 1;
			overflow: hidden;
			position:relative;
			.title,.price{
				font-size:28upx;
				color: #555555;
				height: 40upx;
				line-height: 40upx;
			}
			.title{
				text-overflow: ellipsis;
				white-space: nowrap;
				overflow: hidden;
				font-size: 32upx;
				color: #333333;
				font-weight: bold;
			}
			.attr{
				font-size: 22upx;
				color: #555555;
				height: 32upx;
				line-height: 32upx;
				border-radius: 16upx;
				padding: 0 10upx;
				display: block;
				margin: 20upx 0;
				width: 100upx;
				text-overflow: ellipsis;
				white-space: nowrap;
				overflow: hidden;
				text-align: center;
				&.attr-blue{
					color: #2e8ae5;
					background-color: #eaf5ff;	
				}
				&.attr-red{
					color: #ff7f66;	
					background-color: #fdf1ec;	
				}
			}
			
			.price{
				height: 50upx;
				line-height:50upx;
				font-size: 24upx;
				color: #999999;
				.value{
					font-size: 32upx;
					color: #ff7f66;
					.em{
						font-size: 22upx;
					}
				}
			}
		}
		.del-btn{
			padding:4upx 10upx;
			font-size:34upx; 
			height: 50upx;
			color: #555555;
		}
	}
	/* 底部栏 */
	.action-section{
		/* #ifdef H5 */
		margin-bottom:100upx;
		/* #endif */
		position:fixed;
		left: 0;
		right: 0;
		bottom:0;
		z-index: 95;
		display: flex;
		align-items: center;
		height: 100upx;
		padding: 0 30upx;
		background: rgba(255,255,255,.9);
		box-shadow: 0 0 20upx 0 rgba(0, 0, 0, 0.1);
		.checkbox{
			height:52upx;
			line-height: 52upx;
			position:relative;
			font-size: 0;
			image{
				width: 32upx;
				height: 32upx;
				position:relative;
				z-index: 5;
				vertical-align: middle;
			}
		}
		.clear-btn{
			position:absolute;
			left: 26upx;
			top: 0;
			z-index: 4;
			width: 72upx;
			height: 52upx;
			line-height: 52upx;
			padding-left: 20upx;
			font-size: 28upx;
			color: #333;
			transition: .2s;
			&.show{
				opacity: 1;
				width: 120upx;
			}
		}
		.editBtn{
			position:absolute;
			left: 110upx;
			top: 0;
			z-index: 4;
			width: 72upx;
			height: 52upx;
			line-height: 52upx;
			padding-left: 20upx;
			font-size: 28upx;
			color: #333;
		}
		.total-box{
			flex: 1;
			display:flex;
			flex-direction: column;
			text-align:right;
			padding-right: 40upx;
			.price{
				font-size: 28upx;
				color: #555555;
				text{
					color: #ff7f66;
				}
			}
			.coupon{
				font-size: 28upx;
				color:#555555;
				text{
					color: #555555;
				}
			}
		}
		.editbox{
			flex: 1;
			display:flex;
			text-align:right;
			justify-content: flex-end;
			.collect-btn{
				padding: 0 30upx;
				background: #FFFFFF;
				border: 1px solid #b3b3b3;
				color: #333333;
				margin-right: 30upx;
			}
			.del-btn{
				padding: 0 30upx;
				background: #FFFFFF;
				color: #ff7f66;
				border: 1px solid #ff7f66;
			}
		}
		.confirm-btn{
			padding: 0 60upx;
			margin: 0;
			border-radius: 100px;
			height: 74upx;
			line-height: 74upx;
			font-size: 28upx;
			background: #ff7f66;
		}
		.no-border{
			box-sizing: border-box;
			border: none;
		}
		.btnok{
			background: #FFFFFF;
			color: #007aff;
			border: none;
		}
	}
	/* 复选框选中状态 */
	.action-section .checkbox.checked,
	.cart-item .checkbox.checked{
		color: #555555
	}
</style>
