<template>
  <view class="page-box">
    <view class="bg-color" @click="hideKeyboard"></view>
    <view class="numeric-keyboard">
      <view class="number-display">
        <text>¥</text>
        <text>{{money}}</text>
      </view>
      <view class="keypad">
        <view v-for="button in buttons" :key="button.text" @click="button.onclick">{{ button.text }}</view>
      </view>
    </view>
  </view>
</template>

<script lang="ts">
import type {PropType} from "vue";
import {defineComponent, ref} from "vue";
import {onShow} from "@dcloudio/uni-app";
export default defineComponent({
  props:{
    money: Number,
    showKeyboard:Boolean,
    onSubmit: {
      type:Function as PropType<() => void>
    }
  },
  setup(props,context) {
    const refMoney = ref(props.money ? (props.money / 100).toString() : '0');
    const appendText = (n:number | string) => {
      const nString = n.toString();
      const currentValue = refMoney.value;
      if (currentValue.length >= 13) return;
      const dotIndex = currentValue.indexOf('.');
      if (dotIndex >= 0 && currentValue.length - dotIndex > 2) return;
      if (nString === '.') {
        if (dotIndex >= 0) return;
      } else if (nString === '0') {
        if (dotIndex === -1) {
          if (currentValue === '0') return;
        }
      } else {
        if (currentValue === '0') refMoney.value = '';
      }

      refMoney.value += nString;
    }
    const buttons = [
      {text: "1",onclick: () =>{appendText(1)}},
      {text: "2",onclick: () =>{appendText(2)}},
      {text: "3",onclick: () =>{appendText(3)}},
      {text: "+", onclick: () => {appendText('+')}},
      {text: "4",onclick: () =>{appendText(4)}},
      {text: "5",onclick: () =>{appendText(5)}},
      {text: "6",onclick: () =>{appendText(6)}},
      {text: "-", onclick: () => {appendText('-')}},
      {text: "7",onclick: () =>{appendText(7)}},
      {text: "8",onclick: () =>{appendText(8)}},
      {text: "9",onclick: () =>{appendText(9)}},
      {
        text: "提交",onclick: () =>{
          //判断refMoney是否存在‘+’或者‘-’
          const reg = /\+|\-/g;
          if(reg.test(refMoney.value)){
            const arr = refMoney.value.split(reg);
            const num1 = parseFloat(arr[0]);
            const num2 = parseFloat(arr[1]);
            if(refMoney.value.indexOf('+') >= 0){
              refMoney.value = (num1 + num2).toString();
            }else{
              refMoney.value = (num1 - num2).toString();
            }
          }
          context.emit('money',parseFloat(refMoney.value))
          props.onSubmit?.();
        }},
      {text: ".",onclick: () =>{appendText('.')}},
      {text: "0",onclick: () =>{appendText(0)}},
      {text: "删除",onclick: () =>{refMoney.value = ''}},
    ]
    const refShowKeyboard = ref(false);
    const showKeyboard = () => {
      refShowKeyboard.value = true;
    }
    const hideKeyboard = () => {
      refShowKeyboard.value = false;
      context.emit('onHideKeyboard');
      reset();
    }
    const reset = () => {
      refMoney.value = '0';
    };
    onShow(() => {
      reset();
    });
    return {
      money: refMoney,
      buttons,
      showKeyboard,
      hideKeyboard
    };
  }

})
</script>

<style lang="scss">
.page-box{
  .bg-color{
    background-color: rgba(0,0,0,0.5);
    position: absolute;
    top: 0;
    left: 0;
    height: 100vh;
    width: 100vw;
  }
}
.numeric-keyboard {
  width: 100vw;
  height: 280px;
  position: fixed;
  z-index: 999;
  left: 0;
  bottom: 0;
  .number-display{
    width: 100%;
    padding: 24rpx 24rpx;
    background-color: #fff;
    color: $uni-color-primary;
    font-size: 24px;
    & :last-child{
      margin-left: 12rpx;
    }
  }
}


.keypad {
  display: grid;
  grid-template-areas:
    "one two three addNum"
    "four five six subtractNum"
    "seven eight nine submit"
    "point zero delete submit";
  grid-auto-columns: 1fr;
  grid-auto-rows: 56px;
  background-color: #fff;
  > view {
    text-align: center;
    line-height: 56px;
    color: #333;
    border-top: 1px solid #efefef;
    border-right: 1px solid #efefef;
    &:nth-child(1) {
      grid-area: one;
    }
    &:nth-child(2) {
      grid-area: two;
    }
    &:nth-child(3) {
      grid-area: three;
    }
    &:nth-child(4) {
      grid-area: addNum;
    }
    &:nth-child(5) {
      grid-area: four;
    }
    &:nth-child(6) {
      grid-area: five;
    }
    &:nth-child(7) {
      grid-area: six;
    }
    &:nth-child(8) {
      grid-area: subtractNum;
    }
    &:nth-child(9) {
      grid-area: seven;
    }
    &:nth-child(10) {
      grid-area: eight;
    }
    &:nth-child(11) {
      grid-area: nine;
    }
    &:nth-child(12) {
      grid-area: submit;
      line-height: 112px;
      color: #fff;
      background-color: $uni-color-primary;
    }
    &:nth-child(13) {
      grid-area: point;
    }
    &:nth-child(14) {
      grid-area: zero;
    }
    &:nth-child(15) {
      grid-area: delete;
    }
    &:nth-child(16) {
      grid-area: submit;
    }
  }
}


</style>
