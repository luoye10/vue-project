<script setup lang="ts">
import { reactive, markRaw } from 'vue'
import LikeIcon from '@/assets/icon/LikeIcon.vue';
import MoneyIcon from '@/assets/icon/MoneyIcon.vue'
import CollectIcon from '@/assets/icon/CollectIcon.vue'
import ShareIcon from '@/assets/icon/ShareIcon.vue'

const iconsInfo = reactive([
    { icon: markRaw(LikeIcon), value: '10', isSave: false, shake: false, complete: false },
    { icon: markRaw(MoneyIcon), value: 20, isSave: false, shake: false, complete: false },
    { icon: markRaw(CollectIcon), value: 30, isSave: false, shake: false, complete: false },
    { icon: markRaw(ShareIcon), value: 40, isSave: false, shake: false, complete: false },
])
const timeInfo: {
    dur: number,
    start: number,
    end: number,
    timer: ReturnType<typeof setTimeout> | null
} = {
    dur: 4000,
    start: 0,
    end: 0,
    timer: null
}
const complete = () => {
    iconsInfo.forEach(icon => {
        icon.isSave = icon.shake = false
        icon.complete = true
    })
    console.log('%c效果加载完成，开始发送真正的请求', 'color: #6cf; padding: 10px 15px; font-size: 20px; border: 5px solid #6cf;')
}
const start = () => {
    iconsInfo.forEach(icon => icon.isSave = icon.shake = true)
    timeInfo.timer = setTimeout(() => {
        timeInfo.timer = null
        complete()
    }, timeInfo.dur)
}
const cancel = () => {
    if (timeInfo.timer) {
        clearTimeout(timeInfo.timer)
        iconsInfo.forEach(icon => icon.isSave = icon.shake = false)
        return
    }
}

</script>
<template>
    <div class="box">
        <div class="icon-item" :class="{complete: item.complete}" v-for="item, i in iconsInfo" :key="i" @mousedown="start" @mouseup="cancel">
            <svg width="30" height="30" viewBox="0 0 30 30" class="circle">
                 <circle :class="{'is-save': item.isSave }" cx="15" cy="15" r="14" stroke="#6cf" fill="none" stroke-width="1" ></circle>
            </svg>
            <i class="icon" :class="{shake: item.shake}">
                <component :is="item.icon" />
            </i>
            <span class="num">{{ item.value }}</span>
        </div>
    </div>
</template>
<style lang="scss" scoped>
.box {
    display: flex;
    .icon-item {
        margin: 0 20px;
        display: flex;
        align-items: center;
        cursor: pointer;
        position: relative;
        &.complete {
            color: #6cf;
        }
        .circle{
            position: absolute;
            left: -5px;
            top: -3px;
            circle {
                opacity: 0;
                &.is-save {
                    opacity: 1;
                    transform-origin: 50% 50%;
                    transform: rotate(-90deg);
                    animation: move 4s;
                }
            }
        }
    }
    .icon {
       font-size: 20px;
       height: 20px;
       display: inline-flex;
       &.shake {
            animation: shake 350ms linear infinite reverse;
       }
    }
    .num {
        margin-left: 10px;
    }
}
@keyframes move {
    0% {
        stroke-dasharray: 0 88;
    }
    100% {
        stroke-dasharray: 88 88;
    }
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
</style>
