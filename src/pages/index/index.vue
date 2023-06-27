<template>
	<view class="content">
		<view class="box">
			<view class="box-title">
				<view class="title">支出</view>
				<view><text class="icon">&#xe769;</text></view>
			</view>
			<view class="expend">
				<text class="expend-money">1月支出：1300</text> &nbsp;
				<text class="expend-count">已超支200元</text>
			</view>
			<view class="chart">
				
			</view>
		</view>
		<view class="box">
			<view class="box-title">
				<view class="title">明细</view>
				<view><text class="icon">&#xe769;</text></view>
			</view>
			<view class="chart">
				
			</view>
		</view>
		<view class="box">
			<view class="box-title">
				<view class="title">预算</view>
				<view><text class="icon">&#xe769;</text></view>
			</view>
			<view class="chart">
				
			</view>
		</view>
		<view class="add">
			+
		</view>
	</view>
</template>

<script setup lang="ts">

</script>

<style lang="scss">
	@font-face {
		font-family: 'iconfont';
		src: url('~@/static/iconfont.ttf');
	}
.content{
	margin: 20rpx 15rpx;
	.box{
		border: 1px solid skyblue;
		margin-bottom: 10px;
		.box-title{
				display: flex;
				align-items: center;
				justify-content: space-between;
				.title{
					margin-left: 14px;
					font-size: 12px;
					color: $uni-text-color;
				}
				.icon{
					font-family: iconfont;
					font-size: 20px;
					margin-right: 14px;
					color: $uni-color-primary;
				}
			}
		.expend{
			.expend-money{
				margin-left: 14px;
				font-size: 10px;
				color: #FFC71C;
			}
			.expend-count{
				font-size:8px;
				color: $uni-color-primary;
			}
		}
		.chart{
			background-color: antiquewhite;
			height: 160px;
		}
		}
		.add{
			position: absolute;
			width: 42px;
			height: 42px;
			border-radius: 100%;
			text-align: center;
			line-height: 42px;
			background-color: $uni-color-primary;
			color: #fff;
			right: 20px;
			bottom: 40px;
		}
	}
</style>
