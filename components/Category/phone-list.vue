<template>
	<view>
		<scroll-view class="scroll-list"
		:scroll-top="1"
		scroll-y="true"
		:scroll-with-animation="scrollAnimationOFF" 
		:scroll-into-view="scrollViewId" 
		:style="{height:winHeight + 'px'}" 
		@scroll="handleScroll">
			<view class="phone-list">
				<view  
					v-for="(item, key) of phones" 
					:key="key" 
					:class="key == 'LS' || key == 'RM' ? 'list-item list-item-block':'list-item'"
					:id="key">
					<view class="list-item-title">
						{{key=='LS'?"定位/历史":key=='RM'?"热门":key}}
					</view>
					<view :class="key == 'LS' || key == 'RM' ? 'list-item-phone block-level':'list-item-phone'" 
						@click="handleClick"
						hover-class="commonly-hover" 
						:hover-start-time="20" 
						:hover-stay-time="70" 
						v-for="(innerItem,index) in item"
						:key="innerItem.id"
						:data-name="innerItem.name"
						:data-id="innerItem.id"
						:data-phoneNumber="innerItem.phoneNumber"
					>  
						<image v-if="key == 'LS' && index ==0" src="../../static/image/icon_location.png" mode="" class="address"></image>
						{{innerItem.name}}
					</view>
				</view>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		name:"phone-list",
		props:{
			phones:Object,
			letter:String,
			scrollAnimationOFF:Boolean
		},
		data () {
			return {
				winHeight:0,
				scrollTop:0,
				letterDetails:[],
				timer:null
			}
		},
		computed:{
			scrollViewId () {
				return this.letter
			}
		},
		mounted(){
			// #ifndef APP-PLUS
			this.winHeight = uni.getSystemInfoSync().windowHeight - 49.50
			//#endif
			
			//#ifdef APP-PLUS
			this.winHeight = uni.getSystemInfoSync().windowHeight - 100
			//#endif

		},
		methods:{
			handleClick (e) {
				this.$emit('handleClick',e.target.dataset)
			},
			handleScroll (e){
				this.$nextTick(function(){
					if(this.letterDetails.length === 0){
						let view = uni.createSelectorQuery().selectAll('.list-item')
						view.boundingClientRect(data=>{
							let top = data[0].top
							data.forEach((item,index)=>{
								item.top = item.top - top
								item.bottom  = item.bottom - top
								this.letterDetails.push({
									id:item.id,
									top:item.top,
									bottom:item.bottom
								})
							})
						}).exec()	
					}
					
					const scrollTop = e.detail.scrollTop
					this.letterDetails.some((item,index)=>{
						if(scrollTop>=item.top && scrollTop <= item.bottom - 5){
							this.$emit('change',item.id)
							this.$emit('reset',true)
							return true
						}
					})
				})
			}
		}
			
	}
</script>

<style lang="less">
	
	.commonly-hover{
		background-color: #eee;
	}
	
	.scroll-list{
		flex: 1;
		height: 100vh;
		overflow-y: hidden;
	}

	.phone-list{
		display: flex;
		background-color: #fff;
		flex-direction:column;
		position:relative;
		width: 100%;
	}
	
	.list-item {
		width: 100%;
		display: flex;
		align-items: center;
		flex-wrap:wrap;
		height: 92upx;
		background-color: #fff;
		height: 100%;
		
	}
	
	.list-item >.list-item-phone{
		font-weight: normal;
	}
	.list-item .list-item-phone:last-child:before{
		display: none;
	}
	.list-item-title{
		background-color: #f7f8fa;
		font-size: 28upx;
		color: #999999;
	}
	
	.list-item-title,.list-item-phone{
		width: 100%;
		height: 80upx;
		line-height: 80upx;
		font-size: 28upx;
		color: #555;
		padding: 0 30upx;
		position: relative;
		/* border-bottom: 1px solid #e5e5e5; */
	}
	.list-item-phone:before{
		content: "";
		position: absolute;
		left: 30upx;
		right: 0;
		bottom: 0;
		background: #e5e5e5;
		height: 1px;
	}
	.list-item-block{
		padding: 0 30upx;
		background: #f7f8fa;
		.list-item-title{
			padding: 0;
		}
		.block-level{
			width: 188upx;
			height: 62upx;
			line-height: 62upx;
			border: 1px solid #e5e5e5;
			float: left;
			box-sizing: border-box;
			text-align: center;
			background: #FFFFFF;
			margin-right: 20upx;
			text-overflow: ellipsis;
			white-space: nowrap;
			overflow: hidden;
			&:before{
				display: none;
			}
			&:nth-child(n+5){
				margin-top: 20upx;
			}
			.address{
				width: 20upx;
				height: 24upx;
				display: inline-block;
				margin-right: 6upx;
			}
		}
	}
	
	

</style>
