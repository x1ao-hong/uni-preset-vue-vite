<script setup>
import { ref } from 'vue'

const phone = ref('')
const verifyCode = ref('')
const newPassword = ref('')
const confirmPassword = ref('')
const countdown = ref(0)

// 获取验证码
const getVerifyCode = () => {
  if (!phone.value) {
    uni.showToast({
      title: '请输入手机号',
      icon: 'none'
    })
    return
  }
  // 开始倒计时
  countdown.value = 60
  const timer = setInterval(() => {
    countdown.value--
    if (countdown.value <= 0) {
      clearInterval(timer)
    }
  }, 1000)
  
  // TODO: 调用获取验证码接口
  console.log('获取验证码', phone.value)
}

// 提交修改
const handleSubmit = () => {
  if (!phone.value) {
    uni.showToast({
      title: '请输入手机号',
      icon: 'none'
    })
    return
  }
  if (!verifyCode.value) {
    uni.showToast({
      title: '请输入验证码',
      icon: 'none'
    })
    return
  }
  if (!newPassword.value) {
    uni.showToast({
      title: '请输入新密码',
      icon: 'none'
    })
    return
  }
  if (!confirmPassword.value) {
    uni.showToast({
      title: '请再次输入密码',
      icon: 'none'
    })
    return
  }
  if (newPassword.value !== confirmPassword.value) {
    uni.showToast({
      title: '两次输入的密码不一致',
      icon: 'none'
    })
    return
  }
  
  // TODO: 调用修改密码接口
  console.log('修改密码', {
    phone: phone.value,
    verifyCode: verifyCode.value,
    newPassword: newPassword.value
  })
}

// 返回上一页
const goBack = () => {
  uni.navigateBack()
}
</script>

<template>
  <view class="reset-container">
    <view class="nav-bar">
      <view class="back-icon" @tap="goBack">
        <image src="/static/icons/common/back.png" class="icon" mode="aspectFit" />
      </view>
      <view class="title">修改密码</view>
    </view>
    
    <view class="form-box">
      <view class="form-item">
        <text class="label">手机号</text>
        <input
          class="input"
          type="number"
          v-model="phone"
          placeholder="请输入手机号"
          placeholder-class="placeholder"
        />
      </view>
      
      <view class="form-item verify-code">
        <text class="label">验证码</text>
        <view class="input-box">
          <input
            class="input"
            type="number"
            v-model="verifyCode"
            placeholder="请输入验证码"
            placeholder-class="placeholder"
          />
          <text 
            class="get-code" 
            :class="{ disabled: countdown > 0 }"
            @tap="countdown <= 0 && getVerifyCode()"
          >
            {{ countdown > 0 ? `${countdown}s` : '获取验证码' }}
          </text>
        </view>
      </view>
      
      <view class="form-item">
        <text class="label">新密码</text>
        <input
          class="input"
          type="password"
          v-model="newPassword"
          placeholder="请输入新密码"
          placeholder-class="placeholder"
        />
      </view>
      
      <view class="form-item">
        <text class="label">确认密码</text>
        <input
          class="input"
          type="password"
          v-model="confirmPassword"
          placeholder="请再次输入密码"
          placeholder-class="placeholder"
        />
      </view>
    </view>
    
    <button class="submit-button" @tap="handleSubmit">确定</button>
  </view>
</template>

<style lang="scss" scoped>
.reset-container {
  min-height: 100vh;
  background: url('../../images/background/login-background.jpg') no-repeat center/cover;
  padding: 20rpx 40rpx;
  position: relative;
  box-sizing: border-box;
  display: flex;
  flex-direction: column;
  

  
  .nav-bar {
    position: relative;
    z-index: 1;
    height: 88rpx;
    display: flex;
    align-items: center;
    justify-content: center;
    margin-bottom: 40rpx;
    
    .back-icon {
      position: absolute;
      left: 0;
      width: 88rpx;
      height: 88rpx;
      display: flex;
      align-items: center;
      justify-content: center;
    }
    
    .title {
      font-size: 36rpx;
      color: #333;
      font-weight: 500;
    }
  }

  .form-box {
    position: relative;
    z-index: 1;
    padding: 20rpx 30rpx;
    box-sizing: border-box;
    
    .form-item {
      margin-bottom: 40rpx;
      position: relative;
      
      .label {
        font-size: 28rpx;
        color: #333;
        margin-bottom: 16rpx;
        display: block;
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
        display: flex;
        flex-direction: column;
        
        .input-box {
          display: flex;
          align-items: center;
          gap: 20rpx;
          
          .input {
            flex: 1;
          }
          
          .get-code {
            width: 200rpx;
            height: 88rpx;
            background-color: #3e2723;
            color: #fff;
            font-size: 28rpx;
            border-radius: 12rpx;
            display: flex;
            align-items: center;
            justify-content: center;
            flex-shrink: 0;
            
            &.disabled {
              background-color: #ccc;
            }
            
            &:active {
              opacity: 0.8;
            }
          }
        }
      }
    }
  }

  .submit-button {
    position: relative;
    z-index: 1;
    width: calc(100% - 140rpx);
    height: 88rpx;
    margin: 60rpx auto 0;
    background-color: #3e2723;
    color: #fff;
    font-size: 32rpx;
    border-radius: 12rpx;
    display: flex;
    align-items: center;
    justify-content: center;
    
    &:active {
      opacity: 0.8;
    }
    
    &::after {
      border: none;
    }
  }
}

.placeholder {
  color: #ccc;
}

/* 横屏适配 */
@media screen and (orientation: landscape) {
  .reset-container {
    padding: 20rpx 15vw;
    
    .form-box {
      padding: 20rpx 5vw;
    }
  }
}

/* 小屏幕适配 */
@media screen and (max-height: 600px) {
  .reset-container {
    padding: 20rpx;
    
    .nav-bar {
      height: 80rpx;
      margin-bottom: 30rpx;
      
      .back-icon {
        width: 80rpx;
        height: 80rpx;
      }
      
      .title {
        font-size: 32rpx;
      }
    }
    
    .form-box {
      padding: 20rpx;
      
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
          .get-code {
            height: 80rpx;
            font-size: 26rpx;
          }
        }
      }
    }
    
    .submit-button {
      height: 80rpx;
      font-size: 30rpx;
      margin-top: 40rpx;
    }
  }
}
</style> 