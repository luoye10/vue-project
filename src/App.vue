<script setup lang="ts">
import { ref, reactive } from 'vue'
import LikeIcon from './assets/icon/LikeIcon.vue';
import MoneyIcon from './assets/icon/MoneyIcon.vue'
import CollectIcon from './assets/icon/CollectIcon.vue'
import ShareIcon from './assets/icon/ShareIcon.vue'
const a = ref(43)
const b = ref(26)
const c = ref(78)
const d = ref(16)
const isLike = reactive({v:false})
const isMoney = reactive({v:false})
const isCollect = reactive({v:false})
const isShare = reactive({v:false})
const isShake = reactive({v:false})
const isAdd = ref(false)
const startTime = ref()
const endTime = ref()

function add(){
  isLike.v = !isLike.v
  if(isLike.v === true){
    a.value++
  }else{
    a.value--
  }
}
function triple(){
  startTime.value = new Date().getSeconds()
  isAdd.value = true
  isShake.v = true
  setTimeout(() => isShake.v = false, 4000)
}
function up(){
  endTime.value = new Date().getSeconds()
  let t = endTime.value - startTime.value
  if( t >= 4){
    isLike.v = true
    isMoney.v = true
    isCollect.v = true
    isAdd.value = false
    isShake.v = false
    a.value++
    b.value++
    c.value++
  }else{
    isAdd.value = false
    isLike.v = false
    isShake.v = false
  }
}
function money(){
  if(isLike.v != true){
    add()
  }
  b.value++
  isMoney.v = true
}
function collect(){
  isCollect.v = !isCollect.v
  if(isCollect.v === true){
    c.value++
  }else{
    c.value--
  }
}
function share(){
  d.value++
  isShare.v = true
}
</script>


<template>
  <div class="box">
    <div :class="['item', {active: isLike.v}]" @mousedown="triple" @mouseup="up">
      <LikeIcon :class="['icon', {like: isShake.v}]"></LikeIcon>
      <div :class="{circle:isAdd}">
        <div :class="{'right-circle':isAdd}"></div>
        <div :class="{'left-circle':isAdd}"></div>
      </div>
      <div :class="{ring:isAdd}"></div>
      <div :class="{'bar-box':isAdd}">
       <div :class="{bar:isAdd}"></div>
        <div :class="{bar:isAdd}"></div>
        <div :class="{bar:isAdd}"></div>
        <div :class="{bar:isAdd}"></div>
      </div>
      <div class="num">{{ a }}</div>
    </div>
    <div :class="['item', {active: isMoney.v}]" @click="money">
      <MoneyIcon class="icon"></MoneyIcon>
      <div :class="{circle:isAdd}">
        <div :class="{'right-circle':isAdd}"></div>
        <div :class="{'left-circle':isAdd}"></div>
      </div>
      <div :class="{ring:isAdd}"></div>
      <div :class="{'bar-box':isAdd}">
       <div :class="{bar:isAdd}"></div>
        <div :class="{bar:isAdd}"></div>
        <div :class="{bar:isAdd}"></div>
        <div :class="{bar:isAdd}"></div>
      </div>
      <div class="num">{{ b }}</div>
    </div>
    <div :class="['item',{active: isCollect.v}]" @click="collect">
      <CollectIcon class="icon"></CollectIcon>
      <div :class="{circle:isAdd}">
        <div :class="{'right-circle':isAdd}"></div>
        <div :class="{'left-circle':isAdd}"></div>
      </div>
       <div :class="{ring:isAdd}"></div>
      <div :class="{'bar-box':isAdd}">
        <div :class="{bar:isAdd}"></div>
        <div :class="{bar:isAdd}"></div>
        <div :class="{bar:isAdd}"></div>
        <div :class="{bar:isAdd}"></div>
      </div>
      <div class="num">{{ c }}</div>
    </div>
    <div :class="['item', {active: isShare.v}]" @click="share">
      <ShareIcon class="icon"></ShareIcon>
      <div class="num">{{ d }}</div>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.box{
  display: flex;
  .item{
    display: flex;
    justify-content: center;
    align-items: center;
    margin: 0 20px;
    cursor: pointer;
    position: relative;
    .logo{
      display: flex;
    }
    .icon{
      font-size: 20px;
      margin: auto;
    }
    .num{
      margin-left: 10px;
    }
    &:hover{
      color: #409eff;
    }
    .like{
      animation: shake 350ms linear infinite reverse;
    }
    @keyframes shake {
      // 利用 translate 属性重新定义元素，做到抖动的效果
      10%, 90% { transform: translate3d(-1px, 0, 0); }
      15%, 85% { transform: translate3d(0, -1px, 0); }
      20%, 80% { transform: translate3d(2px, 0, 0); }
      25%, 75% { transform: translate3d(0, 2px, 0); }
      30%, 70% { transform: translate3d(-3px, 0, 0); }
      35%, 65% { transform: translate3d(0, -3px, 0); }
      40%, 60% { transform: translate3d(3px, 0, 0); }
      45%, 55% { transform: translate3d(0, 3px, 0); }
      50% { transform: translate3d(-3px, -3px, 0); }
    }
    .circle{
      width: 40px;
      height: 40px;
      position: absolute;
      left: 50%;
      top: 50%;
      margin-top: -20px;
      margin-left: -34px;
    }
    .right-circle{
      width: 20px;
      height: 40px;
      position: absolute;  
      top: 0;  
      right: 0;
      overflow: hidden;
      &::before{
        content: '';
        width: 40px;
        height: 40px;
        border-radius: 50%;
        border: 2px solid #409eff;
        transform: rotate(45deg);
        border-top-color: transparent;
        border-right-color: transparent;
        animation: rightCircleRotate 4s linear;
        animation-fill-mode: backwards;
        position: absolute;
        top: 0;
        right: 0;
      }
      @keyframes rightCircleRotate {
        0%{
          transform: rotate(45deg);
        }
        50%{
          transform: rotate(225deg);
        }
        100%{
          transform: rotate(225deg);
        }
      }
    }
    .left-circle{
      width: 20px;
      height: 40px;
      position: absolute;  
      top: 0;  
      left: 0;
      overflow: hidden;
      &::before{
        content: '';
        width: 40px;
        height: 40px;
        border-radius: 50%;
        border: 2px solid #409eff;
        transform: rotate(-135deg);
        border-top-color: transparent;
        border-right-color: transparent;
        animation: leftCircleRotate 2s linear;
        animation-fill-mode: backwards;
        animation-delay: 2s;
        position: absolute;
        top: 0;
        left: 0;
      }
      @keyframes leftCircleRotate {
        0%{
          transform: rotate(-135deg);
        }
        100%{
          transform: rotate(45deg);
        }
      }
    }
    .ring{
      width: 40px;
      height: 40px;
      position: absolute;
      left: 50%;
      top: 50%;
      margin-left: -34px;
      margin-top: -20px;
      border: 2px solid #409eff;
      border-radius: 100%;
      opacity: 0;
      animation: ringRotate 0.2s linear;
      animation-fill-mode: forwards;
      animation-delay: 4.1s;
    }
    @keyframes ringRotate {
      0%{
        width: 40px;
        height: 40px;
        opacity: 1;
      }
      100%{
        width: 40px;
        height: 40px;
        opacity: 0;
      }
    }
    .bar-box{
      width: 40px;
      height: 40px;
      border-radius: 100%;
      position: absolute;
      left: 50%;
      top: 50%;
      margin-left: -15px;
      opacity: 0;
      animation: barBoxRotate 1s ;
      animation-fill-mode: forwards;
      animation-delay: 4.2s;
    }
    @keyframes barBoxRotate {
      0%{
        transform: translate(-50%,-50%) scale(0);
      }
      30%{
        opacity: 0;
      }
      70%{
        transform: translate(-50%,-50%) scale(0.9);
        opacity: 1;
      }
      100%{
        transform: translate(-50%,-50%) scale(1);
        opacity: 0;
      }
    }
    .bar{
      width: 40px;
      height: 10px;
      position: absolute;
      top: 50%;
      margin-top: -5px;
      &::before{
        content: '';
        width: 8px;
        height: 4px;
        background: #409eff;
        border-radius: 20px;
        position: absolute;
        left: -10px;
        top: 0;
      }
      &::after{
        content: '';
        width: 8px;
        height: 4px;
        background: #409eff;
        border-radius: 20px;
        position: absolute;
        top: 0;
        right: -10px;
      }
    }
    .bar:nth-child(2){
      transform: rotate(45deg);
    }
    .bar:nth-child(3){
      transform: rotate(90deg);
    }
    .bar:nth-child(4){
      transform: rotate(135deg);
    }
  }
  .active{
    color: #409eff;
  }
}
</style>
