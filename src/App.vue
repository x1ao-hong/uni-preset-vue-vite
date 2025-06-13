<script>
export default {
  onLaunch: function() {
    console.log('App Launch')
    
    // 应用启动时先显示加载页面
    uni.reLaunch({
      url: '/pages/splash/index'
    })
  },
  onShow: function() {
    console.log('App Show')
  },
  onHide: function() {
    console.log('App Hide')
  }
}
</script>

<style lang="scss">
/* 每个页面公共css */
page {
  font-family: -apple-system, BlinkMacSystemFont, 'Helvetica Neue', Helvetica,
    Segoe UI, Arial, Roboto, 'PingFang SC', 'miui', 'Hiragino Sans GB', 'Microsoft Yahei',
    sans-serif;
}

/* 去除按钮的默认边框 */
button::after {
  border: none;
}

/* 统一图片默认样式 */
image {
  vertical-align: middle;
}

/* 输入框placeholder样式 */
.placeholder {
  color: #999;
}

/* 图标基础样式 */
.icon {
  width: 32rpx;
  height: 32rpx;
  
  &.icon-large {
    width: 40rpx;
    height: 40rpx;
  }
  
  &.icon-small {
    width: 24rpx;
    height: 24rpx;
  }
}
</style>
