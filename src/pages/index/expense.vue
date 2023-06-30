<script>
	export default {
		data() {
			return {
				chartData: {},
				areaChartData:{},
				//您可以通过修改 config-ucharts.js 文件中下标为 ['ring'] 的节点来配置全局默认参数，如都是默认参数，此处可以不传 opts 。实际应用过程中 opts 只需传入与全局默认参数中不一致的【某一个属性】即可实现同类型的图表显示不同的样式，达到页面简洁的需求。
				opts: {
					title: {
						name: "总支出",
						fontSize: 12,
						color: "#666666"
					},
					subtitle: {
						name: "¥2000",
						fontSize: 14,
						color: "#7cb5ec"
					}
				}
			};
		},
		onReady() {
			this.getServerData();
		},
		methods: {
			getServerData() {
				//模拟从服务器获取数据时的延时
				setTimeout(() => {
					//模拟服务器返回数据，如果数据格式和标准格式不同，需自行按下面的格式拼接
					let res = {
						series: [{
							data: [{
								"name": "一班",
								"value": 50,
								"labelText":"¥400"
							}, {
								"name":"四班",
								"value":18,
								"labelText":"¥200"
							}, {
								"name": "三班",
								"value": 20,
								"labelText":"¥100"
							}, {
								"name": "四班",
								"value": 18,
								"labelText":"¥800"
							}, {
								"name": "五班",
								"value": 8,
								"labelText":"¥500"
							}]
						}]
					};
					this.chartData = JSON.parse(JSON.stringify(res));
				}, 500);
			},
		},
		onLoad(option) {
			const item = JSON.parse(decodeURIComponent(option.type));
			console.log(item)
			this.areaChartData = JSON.parse(JSON.stringify(item));
		},
	};
</script>

<template>
	<view class="page-box">
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
				<view class="box-title">
					<view class="title">支出趋势</view>
				</view>
				<view class="expend">
					<text class="expend-money">1月支出：1300</text> &nbsp;
					<text class="expend-count">已超支200元</text>
				</view>
				<view class="chart-box" style="height: 25vh;">
					<qiun-data-charts type="cusArea" :chartData="areaChartData" :canvas2d="true"
						canvasId="FLUmWnmGDrbKLqNAtWQMtJxgWJBKDtOn" :ontouch="true" />
				</view>
			</view>
			<view class="box">
				<view class="box-title">
					<view class="title">支出类目</view>
					<view class="category-ctl">
						<text class="category" style="border-right: none;">大类展示</text>
						<text class="category">小类展示</text>
					</view>
				</view>
				<view class="chart-box">
					<qiun-data-charts type="cusRing" :opts="opts" :chartData="chartData" :canvas2d="true"
						canvasId="jouuXgfKblzAYkGejxTNnwFeLKocpeoa" />
				</view>
			</view>
		</view>
	</view>
</template>

<style lang="scss" scoped>
	@import url('~@/static/iconfont.css');

	.page-box {
		background-color: #f5f5f9;
	}

	.content {
		height: 100vh;
		width: calc(100vw - 36px);
		margin: 0 auto;

		.page-ctl {
			padding: 12px 0;
			display: flex;
			font-size: 24rpx;
			justify-content: space-between;

			.date-ctl {
				width: 200rpx;
				height: 28px;
				border-radius: 20px;
				background-color: #fff;
				display: flex;
				align-items: center;
				justify-content: center;
			}

			.type-ctl {
				background-color: #fff;
				width: 160rpx;
				height: 28px;
				border-radius: 20px;
				line-height: 28px;
				text-align: center;
			}
		}
		.box {
			background-color: #fff;
			border-radius: 8px;
			margin-bottom: 10px;
			.box-title {
				display: flex;
				align-items: center;
				justify-content: space-between;
				.title {
					margin-left: 8px;
					margin-top: 8px;
					font-size: 24rpx;
					color: $uni-text-color-grey;
				}
				.category-ctl{
					font-size: 19rpx;
					color: #999;
					margin-right: 16px;
					margin-top: 10px;
					.category{
						border: 1px solid #efefef;
						padding: 3px 4px;
					}
				}
			}

			.expend {
				.expend-money {
					margin-left: 8px;
					font-size: 10px;
					color: #FFC71C;
				}

				.expend-count {
					font-size: 8px;
					color: $uni-color-primary;
				}
			}

			.chart-box {
				width: 100%;
			}
		}
	}

	.icon-right {
		font-family: iconfont;
		font-size: 20px;
		color: $uni-color-primary;
	}
</style>