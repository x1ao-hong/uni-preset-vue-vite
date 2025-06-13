<script setup lang="ts">
import { ref, onMounted } from 'vue'

declare const uni: any

const current = ref(0)



const guideList = [
  {
    title: '享受旅行',
    subtitle: '旅游新时代，开启畅游人生！',
    image: '/static/images/guide/guide1.jpg'
  },
  {
    title: '享受美食',
    subtitle: '美食藏宝图，开启美味之旅',
    image: '/static/images/guide/guide2.jpg'
  },
  {
    title: '享受越西',
    subtitle: '民族瑰宝，薪火相传',
    image: '/static/images/guide/guide3.jpg'
  }
]

const guideImages = [
  '/static/images/guide/guide1.jpg',
  '/static/images/guide/guide2.jpg',
  '/static/images/guide/guide3.jpg'
]

const handleChange = (e) => {
  current.value = e.detail.current
}

const startApp = () => {
  // 存储引导页状态
  uni.setStorageSync('isFirstLaunch', 'false')
  // 跳转到登录页
  uni.reLaunch({
    url: '/pages/login/index'
  })
}

const handleStart = () => {
  uni.redirectTo({
    url: '/pages/login/index'
  });
};
</script>

<template>
  <view class="guide-container">
    <swiper class="guide-swiper" :current="current" @change="handleChange">
      <swiper-item v-for="(item, index) in guideList" :key="index">
        <view class="guide-item">
          <image class="guide-image" :src="item.image" mode="aspectFill" />
          <view class="guide-content">
            <view class="guide-title">{{ item.title }}</view>
            <view class="guide-subtitle">{{ item.subtitle }}</view>
          </view>
        </view>
      </swiper-item>
    </swiper>
    
    <view class="indicator">
      <view 
        class="dot" 
        v-for="(item, index) in guideList" 
        :key="index"
        :class="{ active: current === index }"
      ></view>
    </view>
    
    <view class="start-button" @tap="startApp">立即开启</view>
  </view>
</template>

<style lang="scss" scoped>
.guide-container {
  height: 100vh;
  background: url('/static/images/background/guide-background.png') no-repeat center/cover;
  position: relative;
  overflow: hidden;
  

}

.guide-swiper {
  height: 100%;
}

.guide-item {
  height: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding: 60rpx 40rpx;
  box-sizing: border-box;
  
  .guide-image {
    width: 600rpx;
    height: 600rpx;
    margin: 60rpx 0;
    border-radius: 30rpx;
    box-shadow: 0 8rpx 24rpx rgba(0, 0, 0, 0.1);
  }
  
  .guide-content {
    text-align: center;
    
    .guide-title {
      font-size: 48rpx;
      color: #333;
      font-weight: bold;
      margin-bottom: 20rpx;
    }
    
    .guide-subtitle {
      font-size: 28rpx;
      color: #999;
    }
  }
}

.indicator {
  position: absolute;
  left: 50%;
  bottom: 240rpx;
  transform: translateX(-50%);
  display: flex;
  align-items: center;
  gap: 16rpx;
  
  .dot {
    width: 16rpx;
    height: 16rpx;
    border-radius: 50%;
    background-color: rgba(62, 39, 35, 0.2);
    transition: all 0.3s;
    
    &.active {
      width: 32rpx;
      border-radius: 8rpx;
      background-color: #3e2723;
    }
  }
}

.start-button {
  position: absolute;
  left: 50%;
  bottom: 120rpx;
  transform: translateX(-50%);
  width: 320rpx;
  height: 88rpx;
  background-color: #3e2723;
  color: #fff;
  font-size: 32rpx;
  border-radius: 44rpx;
  display: flex;
  align-items: center;
  justify-content: center;
}
</style> 