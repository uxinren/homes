<script lang="ts">
	export default {}

</script>

<template>
	<view class="page-box">
		<view class="content">
			<view class="tbox" >
				<view class="title">固定支出</view>
				<view class="tlist budget-list">
					<view>
						<view class="amount-box">
							<text>房租</text>
							<text>1500</text>
						</view>
					</view>
					<view>
						<view class="amount-box">
							<text>房租</text>
							<text>1500</text>
						</view>
					</view>
					<view>
						<view class="amount-box">
							<text>房租</text>
							<text>1500</text>
						</view>
					</view>
					<view class="tadd">
						<text class="icon-add">&#xe604;</text>
					</view>
				</view>
			</view>
			<view class="tbox">
				<view class="title">计划支出</view>
				<view class="tlist plan-list">
					<view>
						<view class="amount-box">
							<text>房租</text>
							<text>1500</text>
						</view>
					</view>
					<view>
						<view class="amount-box">
							<text>房租</text>
							<text>1500</text>
						</view>
					</view>
					<view>
						<view class="amount-box">
							<text>房租</text>
							<text>1500</text>
						</view>
					</view>
					<view>
						<view class="amount-box">
							<text>房租</text>
							<text>1500</text>
						</view>
					</view>
					<view class="tadd">
						<text class="icon-add">&#xe604;</text>
					</view>
				</view>
			</view>
			<view class="tbox">
				<view class="title">临时支出</view>
				<view class="tlist temporary-list">
					<view>
						<view class="amount-box">
							<text>房租</text>
							<text>1500</text>
						</view>
					</view>
					<view>
						<view class="amount-box">
							<text>房租</text>
							<text>1500</text>
						</view>
					</view>
					<view>
						<view class="amount-box">
							<text>房租</text>
							<text>1500</text>
						</view>
					</view>
					<view>
						<view class="amount-box">
							<text>房租</text>
							<text>1500</text>
						</view>
					</view>
					<view class="tadd">
						<text class="icon-add">&#xe604;</text>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>


<style lang="scss">
@import url('~@/static/iconfont.css');
$amount-box-count: 9;
.page-box {
	background-color: #f5f5f9;
}

.content {
	height: 100vh;
	margin: 0 auto;
	width: calc(100vw - 36px);
	.tbox{
		.title{
			margin: 20rpx;
		}
		.tlist{
			height: 100%;
			color: #fff;
			font-size: 26rpx;
			display: flex;
			flex-wrap: wrap;
			justify-content: flex-start;
			& > view{
				width: 22%;
				height: 48px;
				border-radius: 12rpx;
				margin-right: 10px;
				margin-bottom: 10px;
				.amount-box{
					display: flex;
					flex-direction: column;
					margin-top: 16rpx;
					margin-left: 16rpx;
				}
			}
			.tadd{
				text-align: center;
				line-height: 48px;
				flex-grow: inherit;
			}
			& :nth-child(4n){
				margin-right: 0;
			}
		}
	}
}
.icon-add{
	font-family: iconfont;
	font-size: 20px;
	color: white;
}

@for $i from 1 through $amount-box-count {
  $color: null; // 初始化颜色变量

  .budget-list > view:nth-child(#{$i}) {
    $color: hsl(calc(360 / $amount-box-count * (#{$i})), 64%, 60%);
    background-color: $color; // 将背景颜色直接应用在选择器内
  }

  .plan-list > view:nth-child(#{$i}) {
    $color: hsl(calc(360 / $amount-box-count * (#{$i + 3})), 64%, 60%);
    background-color: $color; // 将背景颜色直接应用在选择器内
  }

  .temporary-list > view:nth-child(#{$i}) {
    $color: hsl(calc(360 / $amount-box-count * (#{$i + 6})), 64%, 60%);
    background-color: $color; // 将背景颜色直接应用在选择器内
  }
}
</style>