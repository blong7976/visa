<script>
	export default {
		onLaunch: function() {
			// console.log('App Launch')
		},
		onShow: function() {
			// console.log('App Show')
		},
		onHide: function() {
			// console.log('App Hide')
		}
	}
</script>

<style>
	@font-face {
		font-family: yticon;
		font-weight: normal;
		font-style: normal;
		src: url('https://at.alicdn.com/t/font_1078604_w4kpxh0rafi.ttf') format('truetype');
	}
	.yticon {
		font-family: "yticon" !important;
		font-size: 16px;
		font-style: normal;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
	}
	.icon-you:before {
		content: "\e606";
	}
	.icon-xuanzhong2:before {
		content: "\e62f";
	}
	.icon--jianhao:before {
		content: "\e60b";
	}
	.icon-jia2:before {
		content: "\e60a";
	}
	.icon-fanhui:before {
	  content: "\e61b";
	}
	.icon-bianji:before {
		content: "\e646";
	}
	.icon-shouhuodizhi:before {
		content: "\e712";
	}
	
	.clamp1 {
		overflow: hidden;
		text-overflow: ellipsis;
		white-space: nowrap;
		display: block;
	}
	.clamp2 {
		text-overflow: -o-ellipsis-lastline;
		overflow: hidden;
		text-overflow: ellipsis;
		display: -webkit-box;
		-webkit-line-clamp: 2;
		line-clamp: 2;
		-webkit-box-orient: vertical;
	}
</style>
