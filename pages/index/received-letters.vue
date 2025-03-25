<template>
  <view class="page">
    <!-- 顶部标题栏 -->
    <view class="header">
      <text class="title">收到的信</text>
    </view>
    
    <!-- 信件列表 -->
    <view class="letter-list">
      <!-- 暂无数据提示 -->
      <view v-if="letters.length === 0" class="empty-tip">
        <text>暂无收到的信件</text>
      </view>
      
      <!-- 信件列表项 -->
      <view v-else v-for="(letter, index) in letters" :key="index" class="letter-item">
        <view class="letter-content">
          <text class="preview-text">{{ letter.content }}</text>
        </view>
        <view class="letter-info">
          <view class="info-item">
            <text class="label">验证码：</text>
            <text class="value">{{ letter.code }}</text>
          </view>
          <view class="info-item">
            <text class="label">查看次数：</text>
            <text class="value">{{ letter.viewCount }}</text>
          </view>
          <view class="info-item">
            <text class="label">创建时间：</text>
            <text class="value">{{ letter.createTime }}</text>
          </view>
        </view>
      </view>
    </view>
  </view>
</template>

<script setup>
import { ref } from 'vue';

// 信件列表数据
const letters = ref([
  // 示例数据，实际应该从API获取
  {
    content: '这是一封收到的信的内容预览...',
    code: '123456',
    viewCount: 1,
    createTime: '2024-01-20 12:00:00'
  }
]);
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

.letter-list {
  padding: 20px;
  
  .empty-tip {
    text-align: center;
    color: #999;
    padding: 40px 0;
  }
  
  .letter-item {
    background: #f8f8f8;
    border-radius: 10px;
    padding: 15px;
    margin-bottom: 15px;
    
    .letter-content {
      margin-bottom: 10px;
      
      .preview-text {
        font-size: 14px;
        color: #333;
        line-height: 1.5;
      }
    }
    
    .letter-info {
      .info-item {
        display: flex;
        margin-bottom: 5px;
        
        .label {
          font-size: 12px;
          color: #999;
          margin-right: 5px;
        }
        
        .value {
          font-size: 12px;
          color: #666;
        }
      }
    }
  }
}
</style>