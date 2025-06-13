<script setup lang="ts">
import { ref, onMounted } from 'vue'

declare const uni: any

const progress = ref(0)

onMounted(() => {
  const timer = setInterval(() => {
    if (progress.value < 100) {
      progress.value += 1
    } else {
      clearInterval(timer)
      uni.redirectTo({
        url: '/pages/guide/index'
      })
    }
  }, 20) // 2秒加载时间，每20ms增加1%
})
</script>

<template>
  <view class="splash-container">
    <view class="image-wrapper">
      <image src="/static/images/splash-bg.jpg" mode="aspectFit" class="splash-image" />
    </view>
    <view class="loading-bar">
      <view class="progress" :style="{ width: `${progress}%` }"></view>
    </view>
  </view>
</template>

<style lang="scss" scoped>
.splash-container {
  height: 100vh;
  position: relative;
  background-color: #f6f2e6;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  
  .image-wrapper {
    width: 100%;
    height: 70vh; // 图片容器高度，可以根据需要调整
    display: flex;
    justify-content: center;
    align-items: center;
    
    .splash-image {
      width: 100%;
      height: 100%;
      object-fit: contain; // 保持图片比例
    }
  }
  
  .loading-bar {
    position: absolute;
    bottom: 100rpx;
    left: 50%;
    transform: translateX(-50%);
    width: 80%;
    height: 6rpx;
    background-color: rgba(62, 39, 35, 0.2);
    border-radius: 3rpx;
    overflow: hidden;
    
    .progress {
      height: 100%;
      background-color: #3e2723;
      transition: width 0.2s linear;
    }
  }
}
</style> 