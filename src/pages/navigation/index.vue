<template>
  <view class="navigation-container">
    <!-- 顶部搜索栏 -->
    <view class="search-header">
      <view class="back-icon" @tap="goBack">
        <image src="/static/icons/common/back.png" class="icon" mode="aspectFit" />
      </view>
      <view class="search-box">
        <image src="/static/icons/common/search.png" class="icon" mode="aspectFit" />
        <input 
          type="text" 
          v-model="searchKeyword"
          placeholder="搜索目的地" 
          placeholder-class="placeholder"
          @confirm="handleSearch"
        />
      </view>
    </view>

    <!-- 地图区域 -->
    <view class="map-container">
      <map
        class="map"
        :latitude="mapCenter.latitude"
        :longitude="mapCenter.longitude"
        :markers="markers"
        :scale="14"
        @markertap="handleMarkerTap"
      ></map>
    </view>

    <!-- 景点推荐列表 -->
    <view class="spots-container">
      <view class="section-title">景点推荐</view>
      <scroll-view class="spots-list" scroll-x>
        <view 
          class="spot-item" 
          v-for="(spot, index) in spotsList" 
          :key="index"
          @tap="handleSpotClick(spot)"
        >
          <image :src="spot.image" mode="aspectFill" class="spot-image" />
          <view class="spot-info">
            <text class="spot-name">{{ spot.name }}</text>
            <view class="spot-meta">
              <text class="spot-rating">{{ spot.rating }}分</text>
              <text class="spot-distance">{{ spot.distance }}</text>
            </view>
            <text class="spot-desc">{{ spot.description }}</text>
          </view>
        </view>
      </scroll-view>
    </view>
  </view>
</template>

<script setup lang="ts">
import { ref, onMounted } from 'vue'

// 搜索关键词
const searchKeyword = ref('')

// 地图中心点
const mapCenter = ref({
  latitude: 28.135,  // 越西县坐标
  longitude: 102.507
})

// 景点标记点数据
const markers = ref([
  {
    id: 1,
    latitude: 28.135,
    longitude: 102.507,
    iconPath: '/static/icons/common/location-point.png',
    width: 32,
    height: 32,
    callout: {
      content: '越西县',
      padding: 8,
      borderRadius: 4,
      display: 'ALWAYS'
    }
  }
])

// 景点列表数据
const spotsList = ref([
  {
    id: 1,
    name: '凯地里拉温泉',
    image: '/src/static/images/spots/kaidilila.jpg',
    rating: 5.0,
    distance: '800m',
    description: '孕育了独特的人文风情',
    latitude: 28.135,
    longitude: 102.507
  },
  {
    id: 2,
    name: '普雄五彩梯田',
    image: '/src/static/images/spots/puxiong.jpg',
    rating: 4.5,
    distance: '650m',
    description: '孕育了独特的人文风情',
    latitude: 28.140,
    longitude: 102.510
  }
])

// 返回上一页
const goBack = () => {
  uni.navigateBack()
}

// 处理搜索
const handleSearch = (e) => {
  console.log('搜索关键词：', searchKeyword.value)
  // TODO: 实现搜索逻辑
}

// 处理标记点点击
const handleMarkerTap = (e) => {
  const marker = markers.value.find(m => m.id === e.markerId)
  if (marker) {
    console.log('点击了标记点：', marker)
    // TODO: 显示景点详情
  }
}

// 处理景点点击
const handleSpotClick = (spot) => {
  console.log('点击了景点：', spot)
  // 更新地图中心点
  mapCenter.value.latitude = spot.latitude
  mapCenter.value.longitude = spot.longitude
  // TODO: 显示景点详情
}
</script>

<style lang="scss" scoped>
.navigation-container {
  min-height: 100vh;
  background-color: #fff;
  position: relative;
}

.search-header {
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  z-index: 100;
  display: flex;
  align-items: center;
  padding: 20rpx 30rpx;
  background-color: #fff;
  box-shadow: 0 2rpx 10rpx rgba(0,0,0,0.05);
  
  .back-icon {
    width: 88rpx;
    height: 88rpx;
    display: flex;
    align-items: center;
    justify-content: center;
  }
  
  .search-box {
    flex: 1;
    height: 72rpx;
    background-color: #f5f5f5;
    border-radius: 36rpx;
    display: flex;
    align-items: center;
    padding: 0 30rpx;
    margin-left: 20rpx;
    
    .icon {
      margin-right: 10rpx;
    }
    
    input {
      flex: 1;
      font-size: 28rpx;
      color: #333;
    }
  }
}

.map-container {
  width: 100%;
  height: 60vh;
  padding-top: 128rpx;
  
  .map {
    width: 100%;
    height: 100%;
  }
}

.spots-container {
  padding: 30rpx;
  
  .section-title {
    font-size: 32rpx;
    color: #333;
    font-weight: bold;
    margin-bottom: 20rpx;
  }
  
  .spots-list {
    white-space: nowrap;
    
    .spot-item {
      display: inline-block;
      width: 600rpx;
      margin-right: 20rpx;
      border-radius: 12rpx;
      overflow: hidden;
      background-color: #fff;
      box-shadow: 0 2rpx 10rpx rgba(0,0,0,0.05);
      
      &:last-child {
        margin-right: 0;
      }
      
      .spot-image {
        width: 100%;
        height: 320rpx;
      }
      
      .spot-info {
        padding: 20rpx;
        
        .spot-name {
          font-size: 32rpx;
          color: #333;
          font-weight: 500;
          margin-bottom: 10rpx;
        }
        
        .spot-meta {
          display: flex;
          align-items: center;
          margin-bottom: 10rpx;
          
          .spot-rating {
            font-size: 24rpx;
            color: #ff9500;
            margin-right: 20rpx;
          }
          
          .spot-distance {
            font-size: 24rpx;
            color: #999;
          }
        }
        
        .spot-desc {
          font-size: 26rpx;
          color: #666;
          white-space: normal;
          display: -webkit-box;
          -webkit-line-clamp: 2;
          -webkit-box-orient: vertical;
          overflow: hidden;
        }
      }
    }
  }
}

.placeholder {
  color: #999;
}
</style> 