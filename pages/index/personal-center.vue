<template>
  <view class="page">
    <!-- 顶部标题栏 -->
    <view class="header">
      <text class="title">个人中心</text>
    </view>
    
    <!-- 用户信息区域 -->
    <view class="user-info">
      <image class="avatar" src="/static/images/default-avatar.png"></image>
      <view class="user-id">
        <text class="id-label">ID</text>
        <text class="id-value">{{ userId }}</text>
      </view>
    </view>
    
    <!-- 功能列表 -->
    <view class="function-list">
      <view class="function-item" @click="goToMyLetters">
        <view class="item-left">
          <text class="iconfont icon-letter" style="color: #00C853;">✉</text>
          <text class="item-text">我写的信</text>
        </view>
        <text class="iconfont icon-right">></text>
      </view>
      
      <view class="function-item" @click="goToReceivedLetters">
        <view class="item-left">
          <text class="iconfont icon-inbox" style="color: #00C853;">📥</text>
          <text class="item-text">收到的信</text>
        </view>
        <text class="iconfont icon-right">></text>
      </view>
      
      <view class="function-item" @click="goToFAQ">
        <view class="item-left">
          <text class="iconfont icon-question" style="color: #00C853;">❓</text>
          <text class="item-text">常见问题</text>
        </view>
        <text class="iconfont icon-right">></text>
      </view>
    </view>
    
    <!-- 广告区域 -->
    <view class="ad-area">
      <view class="ad-item">
        <!-- 广告内容 -->
      </view>
    </view>
  </view>
</template>

<script setup>
import { ref } from 'vue';

const userId = ref('oAA****Kzk'); // 用户ID

// 跳转到我写的信
const goToMyLetters = () => {
  uni.navigateTo({
    url: '/pages/index/my-letters'
  });
};

// 跳转到收到的信
const goToReceivedLetters = () => {
  uni.navigateTo({
    url: '/pages/index/received-letters'
  });
};

// 跳转到常见问题
const goToFAQ = () => {
  uni.showToast({
    title: '常见问题功能开发中',
    icon: 'none'
  });
};
</script>

<style lang="scss" scoped>
.page {
  min-height: 100vh;
  background-color: #fff;
}

.header {
  padding: 44px 20px 20px;
  text-align: center;
  
  .title {
    font-size: 18px;
    font-weight: bold;
  }
}

.user-info {
  padding: 20px;
  display: flex;
  align-items: center;
  border-bottom: 1px solid #f5f5f5;
  
  .avatar {
    width: 60px;
    height: 60px;
    border-radius: 30px;
    margin-right: 15px;
  }
  
  .user-id {
    .id-label {
      font-size: 14px;
      color: #999;
      margin-right: 5px;
    }
    
    .id-value {
      font-size: 14px;
      color: #333;
    }
  }
}

.function-list {
  padding: 20px;
  
  .function-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    height: 50px;
    margin-bottom: 15px;
    
    .item-left {
      display: flex;
      align-items: center;
      
      .iconfont {
        font-size: 20px;
        margin-right: 10px;
      }
      
      .item-text {
        font-size: 16px;
        color: #333;
      }
    }
    
    .icon-right {
      color: #999;
      font-size: 16px;
    }
  }
}

.ad-area {
  padding: 20px;
  
  .ad-item {
    background-color: #f5f5f5;
    border-radius: 10px;
    height: 100px;
  }
}
</style>