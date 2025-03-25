<template>
  <view class="page">
    <!-- 顶部标题栏 -->
    <view class="header">
      <text class="title">我写的信</text>
    </view>
    
    <!-- 信件列表 -->
    <view class="letter-list">
      <view class="letter-item" v-for="letter in letters" :key="letter.id">
        <view class="letter-content">
          <text class="preview">{{ letter.content }}</text>
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
        <view class="delete-btn" @click="deleteLetter(letter.id)">
          <text class="iconfont">🗑️</text>
        </view>
      </view>
    </view>
  </view>
</template>

<script setup>
import { ref } from 'vue';

// 模拟数据，实际开发时需要从API获取
const letters = ref([
  {
    id: 1,
    content: '你好，这是一封测试信件的内容预览...',
    code: 'VPSZO',
    viewCount: 0,
    createTime: '几秒前'
  },
  {
    id: 2,
    content: '亲爱的朋友，希望你能收到这封信...',
    code: 'MNYPE',
    viewCount: 0,
    createTime: '1天前'
  },
  {
    id: 3,
    content: '这是第三封测试信件的内容...',
    code: 'YLRGB',
    viewCount: 0,
    createTime: '2天前'
  }
]);

// 删除信件
const deleteLetter = (id) => {
  uni.showModal({
    title: '提示',
    content: '确定要删除这封信吗？',
    success: (res) => {
      if (res.confirm) {
        // 实际开发时需要调用API删除
        letters.value = letters.value.filter(item => item.id !== id);
        uni.showToast({
          title: '删除成功',
          icon: 'success'
        });
      }
    }
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

.letter-list {
  padding: 20px;
  
  .letter-item {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 15px;
    margin-bottom: 15px;
    background-color: #f8f8f8;
    border-radius: 10px;
    
    .letter-content {
      flex: 1;
      margin-right: 15px;
      
      .preview {
        font-size: 14px;
        color: #333;
        margin-bottom: 10px;
        display: -webkit-box;
        -webkit-box-orient: vertical;
        -webkit-line-clamp: 2;
        overflow: hidden;
      }
      
      .letter-info {
        .info-item {
          display: flex;
          align-items: center;
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
    
    .delete-btn {
      padding: 10px;
      
      .iconfont {
        font-size: 20px;
        color: #ff4d4f;
      }
    }
  }
}
</style>