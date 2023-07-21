<script>
import index from "@/pages/index/index.vue";

export default {
  data() {
    return {
      selected:0,
      labels: [{
        id: 1,
        myType:0,
        name: "餐饮",
        subclass: [{id: 11, subName: "早餐"}, {id: 12, subName: "中餐"}, {id: 13, subName: "晚餐"}, {id: 14, subName: "下午茶"}, {id: 15, subName: "夜宵"}]
      }, {
        id: 2,
        myType:0,
        name: "娱乐",
        subclass: [{id: 21, subName: "游戏"}, {id: 22, subName: "旅游"}]}, {
        id: 3,
        myType:1,
        name: "家用",
        subclass: [{id: 31, subName: "纸巾"}, {id: 23, subName: "毛巾"}]
      }, {
        id: 4,
        myType:1,
        name: "学习",
        subclass: [{id: 41, subName: "考证"}, {id: 42, subName: "视频课"}]}]
    };
  },
  computed: {
    selectedLabel() {
      const label = this.labels.filter(label => label.myType === this.selected);
      return label ? label : [];
    },
  },
  methods: {
    onTitle(title) {
      this.selected = title
    }
  }
}
</script>

<template>
  <view class="page-box">
    <view class="top-box">
      <view class="income-expenses">
        <text @click="onTitle(0)">支出</text>
        <text @click="onTitle(1)">收入</text>
      </view>
      <view class="center-box">
          <view class="label-wrap" v-for="label in selectedLabel">
              <view class="label-title"><text>{{label.name}}</text></view>
              <view class="label-content">
                <view v-for="subLabel in label.subclass">{{subLabel.subName}}</view>
                <view class="style-add">
                  <navigator open-type="navigate" hover-class='none' url="./class-manage">
                    <text>新增</text>
                  </navigator>
                </view>
              </view>
          </view>
      </view>
    </view>
  </view>
</template>

<style lang="scss">

.page-box {
  height: 100vh;
  background-color: #FDF9FC;
  display: flex;
  color: #333;
  justify-content: center;
}
.top-box{
  width: calc(100vw - 36px);
  margin-top: 12rpx;
 .income-expenses{
   text-align: center;
   margin: 12rpx 0;
   > text{
     padding: 10rpx 48rpx;
     margin: 0 12rpx;
     border-bottom: 1px solid $uni-color-primary;
   }
 }
}
.center-box{
  .label-wrap{
    .label-title{
      font-size: 32rpx;
      color: #666;
      padding-top: 12rpx;
      padding-bottom: 12rpx;
    }
    .label-content{
      padding: 20rpx 12rpx;
      border-radius: 12rpx;
      background-color: #fff;
      display: flex;
      flex-wrap: wrap;
      min-height: 200rpx;
      > view{
        width: 22%;
        margin: 12rpx 3% 12rpx 0;
        height: 60rpx;
        line-height: 60rpx;
        text-align: center;
        border: 1px solid #efefef;
        border-radius: 12rpx;
      }
      & :nth-child(4n){
        margin-right: 0;
      }
      & :last-child{
        color: #ccc;
      }
    }
  }
}
</style>
