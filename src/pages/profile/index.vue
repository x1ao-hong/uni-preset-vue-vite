<template>
    <view class="profile-container">

  
      <!-- 用户信息卡片 -->
      <view class="user-card">
        <view class="user-info">
                  <image class="avatar" src="/static/images/avatar.jpg" mode="aspectFill" />
        <view class="user-details">
          <text class="username">美心的童年</text>
          <text class="phone">177****5642</text>
        </view>
        <view class="settings-icon" @tap="handleSettings">
          <image src="/static/icons/settings.png" class="icon" mode="aspectFit" />
        </view>
        </view>
  
        <!-- 统计数据 -->
        <view class="stats-row">
          <view class="stat-item" @tap="handleStatClick('points')">
            <text class="stat-number">145</text>
            <text class="stat-label">我的点赞</text>
          </view>
          <view class="stat-item" @tap="handleStatClick('locations')">
            <text class="stat-number">15</text>
            <text class="stat-label">我的地址</text>
          </view>
          <view class="stat-item" @tap="handleStatClick('coupons')">
            <text class="stat-number">2</text>
            <text class="stat-label">优惠券</text>
          </view>
          <view class="stat-item" @tap="handleStatClick('balance')">
            <text class="stat-number">87.3</text>
            <text class="stat-label">余额</text>
          </view>
        </view>
      </view>
  
      <!-- 订单状态 -->
      <view class="order-section">
        <view class="order-item" @tap="handleOrderClick('pending')">
          <image src="/static/icons/order-pending.png" class="order-icon" mode="aspectFit" />
          <text class="order-text">待付款</text>
        </view>
        <view class="order-item" @tap="handleOrderClick('paid')">
          <image src="/static/icons/order-paid.png" class="order-icon" mode="aspectFit" />
          <text class="order-text">已付款</text>
        </view>
        <view class="order-item" @tap="handleOrderClick('refund')">
          <image src="/static/icons/order-refund.png" class="order-icon" mode="aspectFit" />
          <text class="order-text">待退款</text>
        </view>
        <view class="order-item" @tap="handleOrderClick('all')">
          <image src="/static/icons/order-all.png" class="order-icon" mode="aspectFit" />
          <text class="order-text">全部订单</text>
        </view>
      </view>
  
      <!-- 常用功能 -->
      <view class="function-section">
        <text class="section-title">常用功能</text>
        
                <view class="function-item" @tap="handleFunctionClick('bankCard')">
          <image src="/static/icons/bank-card.png" class="function-icon" mode="aspectFit" />
          <text class="function-text">银行卡绑定</text>
          <image src="/static/icons/arrow-right.png" class="arrow-icon" mode="aspectFit" />
        </view>

        <view class="function-item" @tap="handleFunctionClick('contact')">
          <image src="/static/icons/contact.png" class="function-icon" mode="aspectFit" />
          <text class="function-text">联系客服</text>
          <image src="/static/icons/arrow-right.png" class="arrow-icon" mode="aspectFit" />
        </view>

        <view class="function-item" @tap="handleFunctionClick('password')">
          <image src="/static/icons/password.png" class="function-icon" mode="aspectFit" />
          <text class="function-text">修改密码</text>
          <image src="/static/icons/arrow-right.png" class="arrow-icon" mode="aspectFit" />
        </view>

        <view class="function-item" @tap="handleFunctionClick('identity')">
          <image src="/static/icons/identity.png" class="function-icon" mode="aspectFit" />
          <text class="function-text">身份认证</text>
          <image src="/static/icons/arrow-right.png" class="arrow-icon" mode="aspectFit" />
        </view>

        <view class="function-item" @tap="handleFunctionClick('favorites')">
          <image src="/static/icons/favorites.png" class="function-icon" mode="aspectFit" />
          <text class="function-text">我的收藏</text>
          <image src="/static/icons/arrow-right.png" class="arrow-icon" mode="aspectFit" />
        </view>

        <view class="function-item" @tap="handleFunctionClick('feedback')">
          <image src="/static/icons/feedback.png" class="function-icon" mode="aspectFit" />
          <text class="function-text">意见反馈</text>
          <image src="/static/icons/arrow-right.png" class="arrow-icon" mode="aspectFit" />
        </view>

        <view class="function-item" @tap="handleFunctionClick('coupon')">
          <image src="/static/icons/coupon.png" class="function-icon" mode="aspectFit" />
          <text class="function-text">优惠券</text>
          <view class="badge">3</view>
          <image src="/static/icons/arrow-right.png" class="arrow-icon" mode="aspectFit" />
        </view>

        <view class="function-item" @tap="handleFunctionClick('points')">
          <image src="/static/icons/points.png" class="function-icon" mode="aspectFit" />
          <text class="function-text">积分商城</text>
          <image src="/static/icons/arrow-right.png" class="arrow-icon" mode="aspectFit" />
        </view>

        <view class="function-item" @tap="handleFunctionClick('invite')">
          <image src="/static/icons/invite.png" class="function-icon" mode="aspectFit" />
          <text class="function-text">邀请好友</text>
          <view class="new-tag">NEW</view>
          <image src="/static/icons/arrow-right.png" class="arrow-icon" mode="aspectFit" />
        </view>

        <view class="function-item" @tap="handleFunctionClick('wallet')">
          <image src="/static/icons/wallet.png" class="function-icon" mode="aspectFit" />
          <text class="function-text">我的钱包</text>
          <image src="/static/icons/arrow-right.png" class="arrow-icon" mode="aspectFit" />
        </view>

        <view class="function-item" @tap="handleFunctionClick('address')">
          <image src="/static/icons/address.png" class="function-icon" mode="aspectFit" />
          <text class="function-text">收货地址</text>
          <image src="/static/icons/arrow-right.png" class="arrow-icon" mode="aspectFit" />
        </view>

        <view class="function-item" @tap="handleFunctionClick('history')">
          <image src="/static/icons/history.png" class="function-icon" mode="aspectFit" />
          <text class="function-text">浏览历史</text>
          <image src="/static/icons/arrow-right.png" class="arrow-icon" mode="aspectFit" />
        </view>

        <view class="function-item" @tap="handleFunctionClick('settings')">
          <image src="/static/icons/settings.png" class="function-icon" mode="aspectFit" />
          <text class="function-text">系统设置</text>
          <image src="/static/icons/arrow-right.png" class="arrow-icon" mode="aspectFit" />
        </view>

        <view class="function-item" @tap="handleFunctionClick('about')">
          <image src="/static/icons/about.png" class="function-icon" mode="aspectFit" />
          <text class="function-text">关于我们</text>
          <image src="/static/icons/arrow-right.png" class="arrow-icon" mode="aspectFit" />
        </view>

        <view class="function-item logout" @tap="handleLogout">
          <image src="/static/icons/logout.png" class="function-icon" mode="aspectFit" />
          <text class="function-text">退出账号</text>
          <image src="/static/icons/arrow-right.png" class="arrow-icon" mode="aspectFit" />
        </view>
      </view>
  

    </view>
  </template>
  
  <script setup lang="ts">
  import { ref } from 'vue'
  
  declare const uni: any
  
  // 处理设置点击
  const handleSettings = () => {
    console.log('设置')
  }
  
  // 处理统计数据点击
  const handleStatClick = (type: string) => {
    console.log('统计点击:', type)
  }
  
  // 处理订单点击
  const handleOrderClick = (type: string) => {
    console.log('订单点击:', type)
  }
  
  // 处理功能点击
  const handleFunctionClick = (type: string) => {
    console.log('功能点击:', type)
    switch (type) {
      case 'password':
        uni.navigateTo({
          url: '/pages/reset-password/index'
        })
        break
      case 'contact':
        uni.showToast({
          title: '客服功能开发中',
          icon: 'none'
        })
        break
      case 'coupon':
        uni.showToast({
          title: '优惠券功能开发中',
          icon: 'none'
        })
        break
      case 'points':
        uni.showToast({
          title: '积分商城功能开发中',
          icon: 'none'
        })
        break
      case 'invite':
        uni.showModal({
          title: '邀请好友',
          content: '邀请好友注册可获得积分奖励，功能开发中...',
          showCancel: false
        })
        break
      case 'wallet':
        uni.showToast({
          title: '钱包功能开发中',
          icon: 'none'
        })
        break
      case 'address':
        uni.showToast({
          title: '收货地址功能开发中',
          icon: 'none'
        })
        break
      case 'history':
        uni.showToast({
          title: '浏览历史功能开发中',
          icon: 'none'
        })
        break
      case 'settings':
        uni.showToast({
          title: '系统设置功能开发中',
          icon: 'none'
        })
        break
      case 'about':
        uni.showModal({
          title: '关于我们',
          content: '越西旅游小程序 v1.0.0\n为您提供最优质的旅游服务体验',
          showCancel: false
        })
        break
      default:
        uni.showToast({
          title: '功能开发中',
          icon: 'none'
        })
    }
  }
  
  // 处理退出登录
  const handleLogout = () => {
    uni.showModal({
      title: '提示',
      content: '确定要退出登录吗？',
      success: (res) => {
        if (res.confirm) {
          uni.removeStorageSync('isLoggedIn')
          uni.removeStorageSync('userRole')
          uni.reLaunch({
            url: '/pages/login/index'
          })
        }
      }
    })
  }
  

  </script>
  
  <style lang="scss" scoped>
  .profile-container {
    min-height: 100vh;
    background-color: #F5F5DC;
    padding-bottom: env(safe-area-inset-bottom);
  }
  
  .user-card {
    background-color: #fff;
    margin: 20rpx 30rpx;
    border-radius: 16rpx;
    padding: 30rpx;
    box-shadow: 0 2rpx 12rpx rgba(0, 0, 0, 0.05);
  }
  
  .user-info {
    display: flex;
    align-items: center;
    margin-bottom: 40rpx;
    
    .avatar {
      width: 120rpx;
      height: 120rpx;
      border-radius: 60rpx;
      margin-right: 24rpx;
    }
    
    .user-details {
      flex: 1;
      
      .username {
        display: block;
        font-size: 32rpx;
        font-weight: 600;
        color: #333;
        margin-bottom: 8rpx;
      }
      
      .phone {
        font-size: 26rpx;
        color: #999;
      }
    }
    
    .settings-icon {
      width: 48rpx;
      height: 48rpx;
      
      .icon {
        width: 100%;
        height: 100%;
      }
    }
  }
  
  .stats-row {
    display: flex;
    justify-content: space-between;
  }
  
  .stat-item {
    text-align: center;
    
    .stat-number {
      display: block;
      font-size: 36rpx;
      font-weight: 600;
      color: #333;
      margin-bottom: 8rpx;
    }
    
    .stat-label {
      font-size: 24rpx;
      color: #666;
    }
  }
  
  .order-section {
    display: flex;
    justify-content: space-around;
    background-color: #fff;
    margin: 20rpx 30rpx;
    border-radius: 16rpx;
    padding: 30rpx 0;
    box-shadow: 0 2rpx 12rpx rgba(0, 0, 0, 0.05);
  }
  
  .order-item {
    display: flex;
    flex-direction: column;
    align-items: center;
    
    .order-icon {
      width: 48rpx;
      height: 48rpx;
      margin-bottom: 12rpx;
    }
    
    .order-text {
      font-size: 24rpx;
      color: #666;
    }
  }
  
  .function-section {
    background-color: #fff;
    margin: 20rpx 30rpx;
    border-radius: 16rpx;
    padding: 30rpx;
    box-shadow: 0 2rpx 12rpx rgba(0, 0, 0, 0.05);
    
    .section-title {
      font-size: 32rpx;
      font-weight: 600;
      color: #333;
      margin-bottom: 30rpx;
    }
  }
  
  .function-item {
    display: flex;
    align-items: center;
    padding: 24rpx 0;
    border-bottom: 1rpx solid #f0f0f0;
    
    &:last-child {
      border-bottom: none;
    }
    
    &.logout {
      .function-text {
        color: #ff4757;
      }
    }
    
    .function-icon {
      width: 40rpx;
      height: 40rpx;
      margin-right: 24rpx;
    }
    
    .function-text {
      flex: 1;
      font-size: 28rpx;
      color: #333;
    }
    
    .badge {
      background-color: #ff4757;
      color: #fff;
      font-size: 20rpx;
      padding: 4rpx 8rpx;
      border-radius: 10rpx;
      margin-right: 16rpx;
      min-width: 32rpx;
      text-align: center;
      line-height: 1;
    }
    
    .new-tag {
      background-color: #ff6b35;
      color: #fff;
      font-size: 18rpx;
      padding: 2rpx 8rpx;
      border-radius: 8rpx;
      margin-right: 16rpx;
      font-weight: bold;
    }
    
    .arrow-icon {
      width: 24rpx;
      height: 24rpx;
    }
  }

  </style>