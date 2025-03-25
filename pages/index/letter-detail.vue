<template>
  <view class="page">
    <!-- 顶部提示 -->
    <view class="tip-box">
      <text class="tip-text">内容由用户自行编辑上传，观点仅代表作者本人。</text>
    </view>
    
    <!-- 信件内容区 -->
    <view class="content">
      <!-- 发信人信息 -->
      <view class="sender-info">
        <text class="sender">微信用户</text>
        <text class="time">1天前</text>
      </view>
      
      <!-- 信件内容 -->
      <view class="letter-content">
        <text class="content-text">你好</text>
      </view>
    </view>

    <!-- 底部区域 -->
    <view class="footer">
      <!-- 回复按钮 -->
      <view class="reply-btn" @click="handleReply">
        <text>回复</text>
      </view>
      
      <!-- 广告区域 -->
      <view class="ad-area">
        <view class="ad-item">
          <!-- 广告内容 -->
        </view>
      </view>
    </view>
  </view>
</template>

<script setup>
import { ref, onMounted } from 'vue';
import { onLoad } from '@dcloudio/uni-app';

// 获取路由参数
const verifyCode = ref('');

// 处理回复
const handleReply = () => {
  uni.showToast({
    title: '回复功能开发中',
    icon: 'none'
  });
};

onLoad((options) => {
  if (options.code) {
    verifyCode.value = options.code;
    // TODO: 根据验证码获取信件详情
    console.log('验证码:', verifyCode.value);
  }
});
</script>

<style lang="scss" scoped>
.page {
  min-height: 100vh;
  background-color: #fff;
  padding-bottom: 120px;
}

.tip-box {
  background-color: #FFF9F0;
  padding: 20rpx;
  
  .tip-text {
    color: #FFA000;
    font-size: 24rpx;
  }
}

.content {
  padding: 30rpx;
}

.sender-info {
  margin-bottom: 30rpx;
  
  .sender {
    font-size: 32rpx;
    font-weight: bold;
    margin-right: 20rpx;
  }
  
  .time {
    font-size: 24rpx;
    color: #999;
  }
}

.letter-content {
  .content-text {
    font-size: 28rpx;
    line-height: 1.6;
    color: #333;
  }
}

.footer {
  position: fixed;
  bottom: 0;
  left: 0;
  width: 100%;
  background-color: #fff;
  padding: 20rpx;
  box-shadow: 0 -2rpx 10rpx rgba(0, 0, 0, 0.05);
  
  .reply-btn {
    background-color: #00C853;
    color: #fff;
    height: 80rpx;
    line-height: 80rpx;
    text-align: center;
    border-radius: 40rpx;
    font-size: 28rpx;
    margin-bottom: 20rpx;
  }
  
  .ad-area {
    .ad-item {
      background-color: #f5f5f5;
      border-radius: 20rpx;
      height: 200rpx;
      // 广告样式
    }
  }
}
</style>