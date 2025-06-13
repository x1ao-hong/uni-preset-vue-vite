<template>
  <view class="schedule-container">
    <view class="content">
      <view class="empty-state">
        <text class="empty-text">暂无行程安排</text>
        <text class="empty-desc">快去首页发现精彩内容吧</text>
      </view>
    </view>
  </view>
</template>

<script setup lang="ts">
declare const uni: any
</script>

<style lang="scss" scoped>
.schedule-container {
  min-height: 100vh;
  background-color: #F5F5DC;
  padding-bottom: env(safe-area-inset-bottom);
}

.content {
  flex: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 100rpx 30rpx;
}

.empty-state {
  text-align: center;
  
  .empty-text {
    display: block;
    font-size: 32rpx;
    color: #666;
    margin-bottom: 16rpx;
  }
  
  .empty-desc {
    font-size: 28rpx;
    color: #999;
  }
}
</style>