<template>
	<view class="content">
		<view class="page-ctl">
			<view class="date-ctl">
				<text class="icon-right">&#xe768;</text>
				<text class="icon">1月</text>
				<text class="icon-right">&#xe769;</text>
			</view>
			<view class="type-ctl">
				<text>支出</text>
				<text>收入</text>
			</view>
		</view>
		<view class="box">
			<view class="chart-box" style="height: 15vh;">
				<qiun-data-charts type="cusArea" :chartData="areaChartData" :canvas2d="true" canvasId="FLUmWnmGDrbKLqNAtWQMtJxgWJBKDtOn" :ontouch="true" />
		</view>
		
	</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				areaChartData:{}
			};
		},
		onLoad(option) {
			const item = JSON.parse(decodeURIComponent(option.type));
			console.log(item)
			this.areaChartData = JSON.parse(JSON.stringify(item));
		},
	}
</script>

<style lang="scss" scoped>
@import url('~@/static/iconfont.css');
.content{
	height: 100vh;
	background-color: #f5f5f9;
	.page-ctl{
		.date-ctl{
			
		}
		.type-ctl{}
	}
}
.icon-right {
	font-family: iconfont;
	font-size: 20px;
	color: $uni-color-primary;
}
</style>
