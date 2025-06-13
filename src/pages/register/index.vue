<script setup lang="ts">
import { ref, reactive } from 'vue'

declare const uni: any

const formData = reactive({
  phone: '',
  code: '',
  password: '',
  inviteCode: ''
})

const counting = ref(0)
let timer: ReturnType<typeof setInterval> | null = null

const startCountdown = () => {
  counting.value = 60
  timer = setInterval(() => {
    if (counting.value > 0) {
      counting.value--
    } else {
      clearInterval(timer!)
      timer = null
    }
  }, 1000)
}

const getVerifyCode = () => {
  if (counting.value > 0) return
  if (!formData.phone) {
    uni.showToast({
      title: '请输入手机号',
      icon: 'none'
    })
    return
  }
  // TODO: 调用获取验证码接口
  startCountdown()
}

const handleRegister = () => {
  if (!formData.phone) {
    uni.showToast({
      title: '请输入手机号',
      icon: 'none'
    })
    return
  }
  if (!formData.code) {
    uni.showToast({
      title: '请输入验证码',
      icon: 'none'
    })
    return
  }
  if (!formData.password) {
    uni.showToast({
      title: '请输入密码',
      icon: 'none'
    })
    return
  }
  
  // TODO: 调用注册接口
  console.log('注册信息', {
    phone: formData.phone,
    verifyCode: formData.code,
    password: formData.password,
    inviteCode: formData.inviteCode
  })
}

const goToLogin = () => {
  uni.navigateBack()
}
</script>

<template>
  <view class="register-container">
    <view class="register-box">
      <view class="register-title">注册账号</view>
      <view class="register-subtitle">注册账号跟我们一起互动吧！</view>
      
      <view class="form-item">
        <view class="label">手机号</view>
        <input 
          class="input" 
          type="number" 
          placeholder="请输入手机号" 
          placeholder-class="placeholder"
          v-model="formData.phone"
        />
      </view>
      
      <view class="form-item verify-code">
        <view class="label">验证码</view>
        <view class="input-box">
          <input 
            class="input" 
            type="number" 
            placeholder="请输入验证码" 
            placeholder-class="placeholder"
            v-model="formData.code"
          />
          <view 
            class="code-btn" 
            :class="{ disabled: counting > 0 }"
            @tap="getVerifyCode"
          >
            {{ counting > 0 ? `${counting}s` : '获取验证码' }}
          </view>
        </view>
      </view>
      
      <view class="form-item">
        <view class="label">密码</view>
        <input 
          class="input" 
          type="password" 
          placeholder="请输入密码" 
          placeholder-class="placeholder"
          v-model="formData.password"
        />
      </view>
      
      <view class="form-item">
        <view class="label">邀请码（非必填）</view>
        <input 
          class="input" 
          type="text" 
          placeholder="请输入邀请码" 
          placeholder-class="placeholder"
          v-model="formData.inviteCode"
        />
      </view>
      
      <button class="submit-btn" @tap="handleRegister">注册</button>
      
      <view class="login-link">
        已有账号？<text @tap="goToLogin">立即登录</text>
      </view>
    </view>
  </view>
</template>

<style lang="scss" scoped>
.register-container {
  min-height: 100vh;
  background: url('../../images/background/login-background.jpg') no-repeat center/cover;
  padding: 20rpx 40rpx;
  position: relative;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  
 
  
  .register-box {
    position: relative;
    z-index: 1;
    width: 100%;
    padding: 20rpx 30rpx;
    box-sizing: border-box;
    
    .register-title {
      font-size: 48rpx;
      color: #333;
      font-weight: bold;
      margin-bottom: 16rpx;
    }
    
    .register-subtitle {
      font-size: 28rpx;
      color: #999;
      margin-bottom: 60rpx;
    }
    
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
      
      &.verify-code {
        .input-box {
          display: flex;
          align-items: center;
          gap: 20rpx;
          
          .input {
            flex: 1;
          }
          
          .code-btn {
            width: 220rpx;
            height: 88rpx;
            background-color: #3e2723;
            color: #fff;
            font-size: 28rpx;
            border-radius: 12rpx;
            display: flex;
            align-items: center;
            justify-content: center;
            
            &.disabled {
              background-color: #cccccc;
            }
          }
        }
      }
    }
    
    .submit-btn {
      width: 100%;
      height: 88rpx;
      background-color: #3e2723;
      color: #fff;
      font-size: 32rpx;
      border-radius: 12rpx;
      display: flex;
      align-items: center;
      justify-content: center;
      margin-top: 60rpx;
      
      &:active {
        opacity: 0.8;
      }
    }
    
    .login-link {
      text-align: center;
      margin-top: 40rpx;
      font-size: 28rpx;
      color: #999;
      
      text {
        color: #3e2723;
        margin-left: 10rpx;
      }
    }
  }
}

.placeholder {
  color: #ccc;
}

/* 横屏适配 */
@media screen and (orientation: landscape) {
  .register-container {
    padding: 20rpx 15vw;
    
    .register-box {
      padding: 20rpx 5vw;
    }
  }
}

/* 小屏幕适配 */
@media screen and (max-height: 600px) {
  .register-container {
    padding: 20rpx;
    
    .register-box {
      padding: 20rpx;
      
      .register-title {
        font-size: 40rpx;
        margin-bottom: 12rpx;
      }
      
      .register-subtitle {
        font-size: 26rpx;
        margin-bottom: 40rpx;
      }
      
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
        
        &.verify-code {
          .input-box {
            .code-btn {
              height: 80rpx;
              font-size: 26rpx;
            }
          }
        }
      }
      
      .submit-btn {
        height: 80rpx;
        font-size: 30rpx;
        margin-top: 40rpx;
      }
      
      .login-link {
        margin-top: 30rpx;
        font-size: 26rpx;
      }
    }
  }
}
</style> 