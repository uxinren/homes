<script lang="ts" setup>
import {ref, computed} from 'vue';
import {onLoad} from "@dcloudio/uni-app";
// 获取路由参数
const amount = ref<number>(0);
onLoad((option) => {
    amount.value = option?.money;
});
const selected = ref<number>(0);
const items: Items[] = [
  {
    id: 1,
    type: 0,
    name: '餐饮',
    item: [
      {id: 11, name: '早餐'},
      {id: 12, name: '中餐'},
      {id: 13, name: '晚餐'},
      {id: 14, name: '下午茶'},
      {id: 15, name: '夜宵'},
    ],
  },
  {
    id: 2,
    type: 0,
    name: '娱乐',
    item: [
      {id: 21, name: '游戏'},
      {id: 22, name: '旅游'}]
  },
  {
    id: 3,
    type: 0,
    name: '家用',
    item: [
      {id: 31, name: '纸巾'},
      {id: 23, name: '毛巾'}],
  },
  {
    id: 4,
    type: 1,
    name: '学习',
    item: [
      {id: 41, name: '考证'},
      {id: 42, name: '视频课'}],
  },
];
const money = ref<number>(0);
const selectedSubLayers = computed(() => {
  const n = items.find((item) => item.id === selected.value);
  return n ? n.item : [];
});

const clickItem = (name:string) => {
  const item = items.find((item) => item.name === name);
  selected.value = item ? item.id : 1;
};
</script>

<template>
  <view class="page-box">
    <form class="content">
      <view class="top-box">
        <view class="input-money">
          <text>¥</text>
          <text>{{amount?amount:0}}</text>
        </view>
        <view class="input-ctl">
          <view class="expenses-ctl">
            <text>{{selected===0?'支出':'收入'}}</text>
            <text class="icon-add">&#xe6c2;</text>
          </view>
          <view class="date-ctl">
            <text>日期</text>
            <text class="icon-add">&#xe799;</text>
          </view>
        </view>
      </view>
      <view class="center-box">
        <view class="center-title" v-for="item in items" :key="item.id">
          <text @click="clickItem(item.name)">{{ item.name }}</text>
        </view>
        <swiper class="center-wrap">
          <swiper-item class="swiper-wrap" v-for="item in items" :key="item.id" :selected="selected">
            <view class="swiper-item" v-for="sublayer in selectedSubLayers" :key="sublayer.id">{{ sublayer.name }}
            </view>
            <view class="all swiper-item">
              <navigator open-type="navigate" hover-class='none' url="./class-manage">
                <text>全部</text>
              </navigator>
            </view>
          </swiper-item>
        </swiper>
      </view>
      <view class="bottom-box">
        <view class="input-text">
          <label style="margin-right: 12px">备注</label>
          <input type="text" placeholder="备注信息" placeholder-style="color:#ccc">
        </view>
        <view style="height: 20vh"></view>
        <button class="add-button" type="primary">保存</button>
      </view>
    </form>
  </view>
</template>


<style lang="scss" scoped>
@import url('~@/static/iconfont.css');

.top-box, .input-money, .input-ctl {
  display: flex;
}

.page-box {
  height: 100vh;
  background-color: #FDF9FC;
}

.content {
  width: 100%;
  height: 100%;

  .top-box {
    height: 15vh;
    background-color: #fff;
    align-items: center;

    > .input-money {
      width: 60%;
      font-size: 72rpx;
      height: 108rpx;
      margin-left: 16px;
      color: $uni-color-primary;

      & :last-child {
        color: #E3B4E4;
        margin-left: 12rpx;
        font-size: 72rpx;
        height: 108rpx;
      }
    }

    > .input-ctl {
      padding-top: 16px;
      line-height: 18rpx;
      color: #ccc;

      .expenses-ctl {
        display: flex;

        & :last-child {
          transform: scale(0.7);
          position: relative;
          margin-bottom: -16rpx;
        }
      }

      .date-ctl {
        margin-left: 12rpx;

        & :last-child {
          margin-right: 8rpx;
        }
      }
    }
  }

  .center-box {
    margin-left: 16px;
    margin-top: 20rpx;

    .center-title {
      float: left;
      margin: 12rpx 28rpx 28rpx 0;
      padding-bottom: 4px;
      font-size: 30rpx;
      border-bottom: 2px solid #FDF9FC;
    }

    .center-wrap {
      height: 30vh;

      .swiper-wrap {
        display: flex;
        align-content: flex-start;
        flex-wrap: wrap;

        .swiper-item {
          width: 20%;
          margin-right: 4%;
          margin-bottom: 28rpx;
          height: 60rpx;
          line-height: 60rpx;
          text-align: center;
          border: 1px solid #efefef;
          border-radius: 20%;
        }

        & :nth-child(4n) {
          margin-right: 0;
        }
      }

    }
  }
}

.bottom-box {
  height: 45vh;
  margin: 0 28rpx;
  display: flex;
  flex-direction: column;
  justify-content: space-between;

  .input-text {
    padding: 20rpx 0;
    display: flex;
    border-bottom: 1px solid #efefef;
  }

  .add-button {
    width: 100%;
    background-color: $uni-color-primary;
  }
}

.css-item-click {
  border-bottom: 2px solid $uni-color-primary;
  color: $uni-color-primary;
}

.all {
  color: #ccc;
}

.icon-add {
  font-family: iconfont;
  font-size: 24rpx;
  text-align: center;
}
</style>
