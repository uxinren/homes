<script lang="ts">
	export default {
		data() {
			return {
				detailList: [{ "date": "01-01", "content": "早餐", "amount": 20, "tag": "固定支出" }, { "date": "01-03", "content": "晚餐", "amount": 70, "tag": "计划支出" }, { "date": "01-04", "content": "买书", "amount": 20, "tag": "临时支出" }],
				areaChartData: [],
				arcbarChartData: {},
				opts:{
					title:{
						name: "¥2000",
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
					let resArea = {
						categories: ["1", "2", "3", "4", "5", "6", "7", "8", "9", "10",
							"11", "12", "13", "14", "15", "16", "17", "18", "19",
							"20", "21", "22", "23", "24", "25", "26", "27", "28", "29", "30", "31"],
						series: [
							{
								name: "支出",
								data: [35, 8, 25, 37, 4, 20, null, null, 400],
								connectNulls: true

							}
						]
					};
					let resArcbar = {
						series: [
							{
								name: "一班",
								data: 0.8
							},
							{
								name: "二班",
								data: 0.6
							},
							{
								name: "三班",
								data: 0.45
							}
						]
					}
					this.areaChartData = JSON.parse(JSON.stringify(resArea));
					this.arcbarChartData = JSON.parse(JSON.stringify(resArcbar));
				}, 500);
			},
		},
	};
</script>
<template>
	<view class="content">
		<view class="box">
			<view class="box-title">
				<view class="title">支出</view>
				<navigator open-type="navigate" hover-class='none' 
				:url="'./statistics?type=' + encodeURIComponent(JSON.stringify(areaChartData))"
				><text class="icon-right">&#xe769;</text></navigator>
			</view>
			<view class="expend">
				<text class="expend-money">1月支出：1300</text> &nbsp;
				<text class="expend-count">已超支200元</text>
			</view>
			<view class="chart-box" style="height: 15vh;">
				<qiun-data-charts type="cusArea" :chartData="areaChartData" :canvas2d="true"
					canvasId="FLUmWnmGDrbKLqNAtWQMtJxgWJBKDtOn" :ontouch="true" />
			</view>
		</view>
		<view class="box">
			<view class="box-title">
				<view class="title">明细</view>
				<navigator open-type="navigate" hover-class='none'
				:url="'./record?type=' + encodeURIComponent(JSON.stringify(areaChartData))"
				><text class="icon-right">&#xe769;</text></navigator>
			</view>
			<view class="chart-box">
				<view v-for="(item,index) in detailList" :key="index" class="list-wraper">
					<view class="circular1"></view>
					<view class="detail-list">
						<view class="content-amount">
							<view class="detail-content">{{item.content}}</view>
							<view class="detail-amount">{{item.amount}}</view>
						</view>
						<view class="date-tag">
							<view class="detail-date">{{item.date}}</view>
							<view class="detail-tag">{{item.tag}}</view>
						</view>
					</view>
				</view>
			</view>
		</view>
		<view class="box">
			<view class="box-title">
				<view class="title">预算</view>
				<navigator open-type="navigate" hover-class='none'
				url="./budget"
				><text class="icon-right">&#xe769;</text></navigator>
			</view>
			<view class="chart-box" style="width: 60vw; height: 25vh;">
				<qiun-data-charts 
					type="cusArcbar"
					:opts="opts"
				    :chartData="arcbarChartData"
				    :canvas2d="true"
				    canvasId="baGBoOciVqbioropKBINPYNKyrrhFHJr"
				 />
				 <view class="budget-tag">
				 	<view class="tag-list">
				 		<view class="tag-wraper">
				 			<view class="circular2" style="background-color: #ea7ccc;"></view>
				 			<view>固定支出</view>
				 		</view>
						<view class="tag-wraper">
							<view class="circular2" style="background-color: #FAC858;"></view>
							<view>计划支出</view>
						</view>
						<view class="tag-wraper">
							<view class="circular2" style="background-color: #73C0DE;"></view>
							<view>临时支出</view>
						</view>
				 	</view>
				 </view>
			</view>
		</view>
		<view class="add">
			<text class="icon-add">&#xe604;</text>
		</view>
	</view>
</template>

<style lang="scss" scoped>
	@import url('~@/static/iconfont.css');
	// @font-face {
	// 	font-family: 'iconfont';
	// 	src: url('~@/static/iconfont.ttf'),
	// 		url('~@/static/iconfont.woff'),
	// 		url('~@/static/iconfont.woff2');
	// }

	.content {
		width: 100vw;
		height: 100vh;
		display: flex;
		flex-direction: column;
		align-items: center;
		background-color: #f5f5f9;

		.box {
			width: calc(100vw - 36px);
			background-color: #fff;
			margin-bottom: 10px;
			padding: 8px;
			border-radius: 8px;
			position: relative;
			.box-title {
				display: flex;
				align-items: center;
				justify-content: space-between;
				margin-bottom: 4px;
				.title {
					margin-left: 8px;
					margin-bottom: 4px;
					font-size: 14px;
					color: $uni-text-color;
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
				.list-wraper {
					display: flex;
					justify-content: flex-start;
					align-items: center;
					.circular1 {
						width: 10rpx;
						height: 10rpx;
						border-radius: 10rpx;
						margin: 16rpx;
						background-color: $uni-color-primary;
					}

					.detail-list {
						width: 100%;
						font-size: 20rpx;
						line-height: 20rpx;
						color: #333;
						padding-top: 12rpx;
						padding-bottom: 12rpx;

						.content-amount {
							display: flex;
							width: 95%;
							justify-content: space-between;
							align-items: center;

							.detail-content {
								font-size: 28rpx;
								line-height: 28rpx;
								color: #333;
							}
							.detail-amount{
								font-size: 28rpx;
							}
						}

						.date-tag {
							display: flex;
							width: 98%;
							justify-content: space-between;
							align-items: center;
							color: #999;

							.detail-tag {
								padding: 4px;
								border: 1px solid #efefef;
								border-radius: 4px;
								transform: scale(0.8);
							}
						}
					}
				}
				.budget-tag{
					position: absolute;
					right: 140rpx;
					top: 120rpx;
					font-size: 24rpx;
					.tag-list{
						.tag-wraper{
							display: flex;
							align-items: center;
							margin-top: 32rpx;
							.circular2{
								width: 20rpx;
								height: 20rpx;
								border-radius: 10rpx;
								margin-right: 12rpx;
							}
						}
					}
				}
			}
		}

		.add {
			position: fixed;
			width: 42px;
			height: 42px;
			border-radius: 100%;
			text-align: center;
			line-height: 42px;
			background-color: $uni-color-primary;
			color: #fff;
			box-shadow: 0 6px 10px 0 rgba(0, 0, 0, 0.15), 0 6px 12px 0 rgba(0, 0, 0, 0.15);
			right: 30rpx;
			bottom: 100rpx;
		}
	}
.icon-right {
	font-family: iconfont;
	font-size: 20px;
	margin-right: 14px;
	color: $uni-color-primary;
}
.icon-add{
	font-family: iconfont;
	font-size: 20px;
	color: white;
}
</style>