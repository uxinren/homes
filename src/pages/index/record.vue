<script lang="ts">
	export default {
		data() {
			return {
				detailList: [
				{ "date": "01-01", "content": "早餐", "amount": 20, "tag": "固定支出" }, 
				{ "date": "01-03", "content": "晚餐", "amount": 70, "tag": "计划支出" },
				{ "date": "01-04", "content": "买书", "amount": 20, "tag": "临时支出" }],
			};
		},
	}
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
					<view>全部</view>
				</view>
			</view>
			<view class="total">
				<view class="expenses">
					<text>支出</text>
					<text>-120</text>
				</view>
				<view class="income">
					<text>收入</text>
					<text>100</text>
				</view>
				<view class="net-income">
					<text>净收入</text>
					<text>20</text>
				</view>
			</view>
			<view class="detail">
				<view class="title">收支明细</view>
				<view class="detail-box">
					<view class="detail-wraper">
						<view class="date-day">1月1日&nbsp;星期四</view>
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
	.total{
		height: 16vh;
		display: flex;
		justify-content: center;
		align-items: center;
		border-radius: 8px;
		background-image: linear-gradient(-45deg, #FF68B0, #FF907C);
		& > view{
			margin: 0 72rpx;
			line-height: 60rpx;
			color: #fff;
			font-size: 28rpx;
			display: flex;
			flex-direction: column;
		}
	}
	.detail{
		.title{
			margin: 20px 0 10px 0;
		}
		.detail-box{
			background-color: #fff;
			padding: 10px 8px;
			.detail-wraper{
				border-bottom: 1px dashed $uni-color-primary;
				.date-day{
					font-size: 24rpx;
					color: #999;
					padding-bottom: 4px;
					padding-left: 6px;
				}
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
			}
		}
	}
}
.icon-right {
	font-family: iconfont;
	font-size: 20px;
	color: $uni-color-primary;
}
</style>