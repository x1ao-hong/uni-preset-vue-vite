<template>
  <view class="nearby-container">
    <view class="content">
      <view class="empty-state">
        <image src="/static/icons/empty-nearby.png" class="empty-icon" mode="aspectFit" />
        <text class="empty-text">暂无周边信息</text>
        <text class="empty-desc">正在为您搜索附近的精彩内容</text>
      </view>
    </view>
  </view>
</template>

<script setup lang="ts">
declare const uni: any
</script>

<style lang="scss" scoped>
.nearby-container {
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
  
  .empty-icon {
    width: 200rpx;
    height: 200rpx;
    margin-bottom: 40rpx;
  }
  
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