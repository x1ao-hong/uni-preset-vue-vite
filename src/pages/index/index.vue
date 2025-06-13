<template>
  <view class="home-container">
    <!-- 顶部搜索区域 -->
    <view class="search-header">
      <view class="location">
        大理市 <image src="/static/icons/common/arrow.png" class="icon icon-small" mode="aspectFit" />
      </view>
      <view class="search-box">
        <image src="/static/icons/common/search.png" class="icon" mode="aspectFit" />
        <input type="text" placeholder="请输入关键词" placeholder-class="placeholder" />
      </view>
      <view class="screen-icon">
        <image src="/static/icons/common/filter.png" class="icon icon-large" mode="aspectFit" />
      </view>
    </view>

    <!-- 功能导航区域 -->
    <view class="nav-section">
      <view class="nav-item" v-for="(item, index) in navList" :key="index" @tap="handleNavClick(item)">
        <image :src="item.icon" mode="aspectFit" class="nav-icon" />
        <text class="nav-text">{{ item.name }}</text>
      </view>
    </view>

    <!-- 热门推荐区域 -->
    <view class="section">
      <view class="section-header">
        <text class="section-title">热门推荐</text>
        <view class="more" @tap="handleViewMore('hot')">
          全部 <image src="/static/icons/common/arrow.png" class="icon icon-small" mode="aspectFit" />
        </view>
      </view>
      <view class="hot-list">
        <view class="hot-item large" @tap="handleHotItemClick(hotList[0])">
          <image :src="hotList[0].image" mode="aspectFill" class="hot-image" />
          <view class="hot-info">
            <text class="hot-title">{{ hotList[0].title }}</text>
            <text class="hot-price">¥{{ hotList[0].price }}起</text>
          </view>
        </view>
        <view class="hot-right">
          <view class="hot-item small" v-for="(item, index) in hotList.slice(1)" :key="index" @tap="handleHotItemClick(item)">
            <image :src="item.image" mode="aspectFill" class="hot-image" />
            <view class="hot-info">
              <text class="hot-title">{{ item.title }}</text>
              <text class="hot-price">¥{{ item.price }}起</text>
            </view>
          </view>
        </view>
      </view>
    </view>

    <!-- 目的地推荐区域 -->
    <view class="section">
      <view class="section-header">
        <text class="section-title">目的地推荐</text>
        <view class="more" @tap="handleViewMore('destination')">
          全部 <image src="/static/icons/common/arrow.png" class="icon icon-small" mode="aspectFit" />
        </view>
      </view>
      <scroll-view class="tag-scroll" scroll-x>
        <view 
          class="tag-item" 
          v-for="(tag, index) in destinationTags" 
          :key="index"
          :class="{ active: currentTag === tag }"
          @tap="handleTagClick(tag)"
        >
          {{ tag }}
        </view>
      </scroll-view>
      <view class="destination-list">
        <view 
          class="destination-item"
          v-for="(item, index) in destinationList"
          :key="index"
          @tap="handleDestinationClick(item)"
        >
          <image :src="item.image" mode="aspectFill" class="destination-image" />
          <view class="destination-info">
            <text class="destination-title">{{ item.title }}</text>
            <text class="destination-desc">{{ item.description }}</text>
          </view>
        </view>
      </view>
    </view>


  </view>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'


declare const uni: any

// 检查登录状态
onMounted(() => {
  const isLoggedIn = uni.getStorageSync('isLoggedIn')
  if (!isLoggedIn) {
    uni.redirectTo({
      url: '/pages/login/index'
    })
    return
  }
})

// 导航列表数据
const navList = ref([
  { name: '出行', icon: '/static/icons/nav/travel.png' },
  { name: '美食', icon: '/static/icons/nav/food.png' },
  { name: '住宿', icon: '/static/icons/nav/hotel.png' },
  { name: '文创', icon: '/static/icons/nav/culture.png' },
  { name: '发现', icon: '/static/icons/nav/discover.png' },
  { name: '公告', icon: '/static/icons/nav/notice.png' }
])

// 热门推荐数据
const hotList = ref([
  {
    title: '大理俊发铂尔曼酒店 3天2晚住宿+餐饮',
    price: '1200',
    image: '/static/images/spots/dalijiudian.jpg'
  },
  {
    title: '大理古城鸿隆半山酒店',
    price: '585',
    image: '/static/images/spots/honglong.jpg'
  },
  {
    title: '浅语小院民宿',
    price: '256',
    image: '/static/images/spots/qianyuxiaoyuan.jpg'
  }
])

// 目的地标签
const destinationTags = ref(['精选', '大理古城', '苍山', '洱海', '喜洲古镇', '文笔村'])
const currentTag = ref('精选')

// 目的地列表
const destinationList = ref([
  {
    title: '大理古城',
    description: '历史悠久文化古城',
    image: '/static/images/spots/dali.jpg'
  },
  {
    title: '苍山',
    description: '19峰18溪景色秀丽',
    image: '/static/images/spots/cangshang.jpg'
  },
  {
    title: '洱海',
    description: '高原湖泊，湖水清澈',
    image: '/static/images/spots/erhai.jpg'
  },
  {
    title: '喜洲古镇',
    description: '白族民居建筑群',
    image: '/static/images/spots/xizhou.jpg'
  },
  {
    title: '文笔村',
    description: '白族村落，风景如画',
    image: '/static/images/spots/wenbicai.jpg'
  }
])

// 处理导航点击
const handleNavClick = (item: any) => {
  console.log('导航点击:', item.name)
}

// 处理查看更多
const handleViewMore = (type: string) => {
  console.log('查看更多:', type)
}

// 处理热门项目点击
const handleHotItemClick = (item: any) => {
  console.log('热门项目点击:', item.title)
}

// 处理标签点击
const handleTagClick = (tag: string) => {
  currentTag.value = tag
}

// 处理目的地点击
const handleDestinationClick = (item: any) => {
  console.log('目的地点击:', item.title)
}

// 处理飞行按钮点击
const handleFlyClick = () => {
  uni.navigateTo({
    url: '/pages/navigation/index'
  })
}
</script>

<style lang="scss" scoped>
.home-container {
  min-height: 100vh;
  background-color: #F5F5DC;
  padding-bottom: env(safe-area-inset-bottom);
}

// 顶部搜索区域
.search-header {
  display: flex;
  align-items: center;
  padding: 20rpx 30rpx;
  background-color: #f5f5f5;
  
  .location {
    font-size: 32rpx;
    color: #333;
    margin-right: 20rpx;
    display: flex;
    align-items: center;
    
    .icon {
      margin-left: 4rpx;
    }
  }
  
  .search-box {
    flex: 1;
    height: 72rpx;
    background-color: #f5f5f5;
    border-radius: 36rpx;
    display: flex;
    align-items: center;
    padding: 0 30rpx;
    
    .icon {
      margin-right: 10rpx;
    }
    
    input {
      flex: 1;
      font-size: 28rpx;
      color: #333;
    }
  }
  
  .screen-icon {
    margin-left: 20rpx;
    width: 72rpx;
    height: 72rpx;
    display: flex;
    align-items: center;
    justify-content: center;
  }
}

// 导航区域
.nav-section {
  display: flex;
  flex-wrap: wrap;
  padding: 30rpx;
  background-color: #f5f5f5;
  margin-top: 20rpx;
  
  .nav-item {
    width: 16.666%;
    display: flex;
    flex-direction: column;
    align-items: center;
    margin-bottom: 20rpx;
    
    .nav-icon {
      width: 80rpx;
      height: 80rpx;
      margin-bottom: 10rpx;
    }
    
    .nav-text {
      font-size: 24rpx;
      color: #333;
    }
  }
}

// 公共section样式
.section {
  margin-top: 20rpx;
  background-color: #f5f5f5;
  padding: 30rpx;
  
  .section-header {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 20rpx;
    
    .section-title {
      font-size: 32rpx;
      color: #333;
      font-weight: bold;
      position: relative;
      padding-left: 20rpx;
      
      &::before {
        content: '';
        position: absolute;
        left: 0;
        top: 50%;
        transform: translateY(-50%);
        width: 8rpx;
        height: 32rpx;
        background-color: #3e2723;
        border-radius: 4rpx;
      }
    }
    
    .more {
      font-size: 28rpx;
      color: #999;
      display: flex;
      align-items: center;
      
      .icon {
        margin-left: 4rpx;
      }
    }
  }
}

// 热门推荐区域
.hot-list {
  display: flex;
  gap: 20rpx;
  
  .hot-item {
    position: relative;
    border-radius: 12rpx;
    overflow: hidden;
    
    &.large {
      width: 400rpx;
      height: 400rpx;
    }
    
    &.small {
      width: 250rpx;
      height: 190rpx;
      margin-bottom: 20rpx;
      
      &:last-child {
        margin-bottom: 0;
      }
    }
    
    .hot-image {
      width: 100%;
      height: 100%;
    }
    
    .hot-info {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      padding: 20rpx;
      background: linear-gradient(to top, rgba(0,0,0,0.6), transparent);
      
      .hot-title {
        font-size: 28rpx;
        color: #fff;
        margin-bottom: 10rpx;
        display: block;
      }
      
      .hot-price {
        font-size: 24rpx;
        color: #fff;
      }
    }
  }
  
  .hot-right {
    flex: 1;
    display: flex;
    flex-direction: column;
  }
}

// 目的地推荐区域
.tag-scroll {
  white-space: nowrap;
  margin: 0 -30rpx;
  padding: 0 30rpx;
  margin-bottom: 20rpx;
  
  .tag-item {
    display: inline-block;
    padding: 12rpx 30rpx;
    font-size: 28rpx;
    color: #666;
    background-color: #f5f5f5;
    border-radius: 28rpx;
    margin-right: 20rpx;
    
    &.active {
      color: #fff;
      background-color: #3e2723;
    }
    
    &:last-child {
      margin-right: 0;
    }
  }
}

.destination-list {
  .destination-item {
    margin-bottom: 20rpx;
    border-radius: 12rpx;
    overflow: hidden;
    position: relative;
    
    &:last-child {
      margin-bottom: 0;
    }
    
    .destination-image {
      width: 100%;
      height: 300rpx;
    }
    
    .destination-info {
      position: absolute;
      left: 0;
      right: 0;
      bottom: 0;
      padding: 20rpx;
      background: linear-gradient(to top, rgba(0,0,0,0.6), transparent);
      
      .destination-title {
        font-size: 32rpx;
        color: #fff;
        margin-bottom: 8rpx;
        display: block;
      }
      
      .destination-desc {
        font-size: 24rpx;
        color: rgba(255,255,255,0.8);
      }
    }
  }
}



.placeholder {
  color: #999;
}
</style> 