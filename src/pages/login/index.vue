<script setup>
import { ref } from 'vue'

const phone = ref('')
const password = ref('')

const handleLogin = () => {
  if (!phone.value) {
    uni.showToast({
      title: '请输入手机号',
      icon: 'none'
    })
    return
  }
  if (!password.value) {
    uni.showToast({
      title: '请输入密码',
      icon: 'none'
    })
    return
  }

  // =====================================================
  // TODO: 测试账号，上线前删除
  // 管理员测试账号：
  // 手机号：admin
  // 密码：123456
  // =====================================================
  if (phone.value === '123456' && password.value === '123456') {
    uni.showToast({
      title: '登录成功',
      icon: 'success'
    })
    // 存储登录状态
    uni.setStorageSync('isLoggedIn', 'true')
    uni.setStorageSync('userRole', 'admin')
    // 延迟跳转，让用户看到成功提示
    setTimeout(() => {
      uni.reLaunch({
        url: '/pages/index/index'
      })
    }, 1500)
    return
  }
  // =====================================================
  // TODO: 以下是正式的登录逻辑，上线时启用
  // =====================================================
  console.log('登录信息：', {
    phone: phone.value,
    password: password.value
  })
  // 实现实际的登录逻辑
  uni.showToast({
    title: '账号或密码错误',
    icon: 'none'
  })
}

const handleRegister = () => {
  uni.navigateTo({
    url: '/pages/register/index'
  })
}

const handleForgotPassword = () => {
  uni.navigateTo({
    url: '/pages/reset-password/index'
  })
}

const handleWechatLogin = () => {
  // TODO: 实现微信登录
  console.log('微信登录')
}
</script>

<template>
  <view class="login-container">
    <view class="login-box">
      <view class="login-title">登录账号</view>
      <view class="login-subtitle">赶快登录属于你的账号吧！</view>
      
      <view class="login-form">
        <view class="form-item">
          <view class="label">手机号</view>
          <input
            class="input"
            type="number"
            v-model="phone"
            placeholder="请输入手机号"
            placeholder-class="placeholder"
          />
        </view>
        <view class="form-item">
          <view class="label">密码</view>
          <input
            class="input"
            type="password"
            v-model="password"
            placeholder="请输入密码"
            placeholder-class="placeholder"
          />
        </view>
        
        <view class="forgot-password" @tap="handleForgotPassword">
          忘记密码?
        </view>

        <view class="button-group">
          <button class="register-button" @tap="handleRegister">注册</button>
          <button class="login-button" @tap="handleLogin">登录</button>
        </view>
      </view>

      <view class="other-login">
        <view class="divider">
          <text class="divider-text">合作账号登录</text>
        </view>
        <view class="wechat-login" @tap="handleWechatLogin">
          <image src="/src/images/wechat/wechat.png" mode="aspectFit" class="wechat-icon" />
        </view>
      </view>
    </view>
  </view>
</template>

<style lang="scss" scoped>
.login-container {
  min-height: 100vh;
  background: url('../../images/background/login-background.jpg') no-repeat center/cover;
  padding: 20rpx 40rpx;
  position: relative;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  

}

.login-box {
  position: relative;
  z-index: 1;
  width: 100%;
  padding: 20rpx 30rpx;
  box-sizing: border-box;
}

.login-title {
  font-size: 48rpx;
  color: #333;
  font-weight: bold;
  margin-bottom: 16rpx;
}

.login-subtitle {
  font-size: 28rpx;
  color: #999;
  margin-bottom: 60rpx;
}

.login-form {
  .form-item {
    margin-bottom: 40rpx;
    
    .label {
      font-size: 28rpx;
      color: #333;
      margin-bottom: 16rpx;
    }

    .input {
      width: 100%;
      height: 88rpx;
      background-color: #f8f4f0;
      border-radius: 12rpx;
      padding: 0 30rpx;
      box-sizing: border-box;
      font-size: 28rpx;
      color: #333;
    }
  }

  .forgot-password {
    text-align: right;
    font-size: 28rpx;
    color: #3e2723;
    margin: 20rpx 0 60rpx;
  }

  .button-group {
    display: flex;
    gap: 20rpx;
    margin-bottom: 60rpx;

    button {
      flex: 1;
      height: 88rpx;
      font-size: 32rpx;
      border-radius: 12rpx;
      display: flex;
      align-items: center;
      justify-content: center;
      
      &::after {
        border: none;
      }
      
      &:active {
        opacity: 0.8;
      }
    }

    .register-button {
      background-color: #f8f4f0;
      color: #3e2723;
      border: 2rpx solid #3e2723;
    }

    .login-button {
      background-color: #3e2723;
      color: #fff;
    }
  }
}

.other-login {
  .divider {
    position: relative;
    text-align: center;
    margin-bottom: 40rpx;
    
    &::before,
    &::after {
      content: '';
      position: absolute;
      top: 50%;
      width: 30%;
      height: 1px;
      background-color: rgba(62, 39, 35, 0.2);
    }
    
    &::before {
      left: 0;
    }
    
    &::after {
      right: 0;
    }
    
    .divider-text {
      display: inline-block;
      padding: 0 30rpx;
      font-size: 24rpx;
      color: #999;
      background-color: transparent;
    }
  }

  .wechat-login {
    display: flex;
    justify-content: center;
    position: relative;
    
    .wechat-icon {
      width: 80rpx;
      height: 80rpx;
      border-radius: 50%;
      padding: 15rpx;
      box-sizing: border-box;
      background-color: #f8f4f0;
      
      &::before {
        content: '微信';
        position: absolute;
        bottom: -40rpx;
        left: 50%;
        transform: translateX(-50%);
        font-size: 24rpx;
        color: #999;
        white-space: nowrap;
      }
    }
  }
}

.placeholder {
  color: #ccc;
}

/* 横屏适配 */
@media screen and (orientation: landscape) {
  .login-container {
    padding: 20rpx 15vw;
    
    .login-box {
      padding: 20rpx 5vw;
    }
  }
}

/* 小屏幕适配 */
@media screen and (max-height: 600px) {
  .login-container {
    padding: 20rpx;
    
    .login-box {
      padding: 20rpx;
      
      .login-title {
        font-size: 40rpx;
        margin-bottom: 12rpx;
      }
      
      .login-subtitle {
        font-size: 26rpx;
        margin-bottom: 40rpx;
      }
      
      .login-form {
        .form-item {
          margin-bottom: 30rpx;
          
          .label {
            font-size: 26rpx;
            margin-bottom: 12rpx;
          }
          
          .input {
            height: 80rpx;
            font-size: 26rpx;
          }
        }
        
        .forgot-password {
          font-size: 26rpx;
          margin: 16rpx 0 40rpx;
        }
        
        .button-group {
          margin-bottom: 40rpx;
          
          button {
            height: 80rpx;
            font-size: 30rpx;
          }
        }
      }
    }
  }
}
</style> 