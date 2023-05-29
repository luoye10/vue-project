<script setup lang="ts">
import { ref, reactive } from 'vue'
import LikeIcon from './assets/icon/LikeIcon.vue';
import MoneyIcon from './assets/icon/MoneyIcon.vue'
import CollectIcon from './assets/icon/CollectIcon.vue'
import ShareIcon from './assets/icon/ShareIcon.vue'
const a = ref(143)
const b = ref(26)
const c = ref(78)
const d = ref(162)
const isAdd = ref(false)
const flag = reactive({v:false})

function add(){
  a.value++
  b.value++
  c.value++ 
  isAdd.value = true
}
function share(){
  d.value++
  flag.v = true
}
</script>

<template>
  <div class="box">
    <div :class="['item', {active: isAdd}]" @click="add">
      <LikeIcon class="icon"></LikeIcon>
      <div class="num">{{ a }}</div>
    </div>
    <div :class="['item', {active: isAdd}]" @click="add">
      <MoneyIcon class="icon"></MoneyIcon>
      <div class="num">{{ b }}</div>
    </div>
    <div :class="['item', {active: isAdd}]" @click="add">
      <CollectIcon class="icon"></CollectIcon>
      <div class="num">{{ c }}</div>
    </div>
    <div :class="['item', {active: flag.v}]" @click="share">
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
    .icon{
      font-size: 25px;
    }
    .num{
      margin-left: 5px;
    }
    &:hover{
      color: #409eff;
    }
  }
  .active{
    color: #409eff;
  }
}
</style>
