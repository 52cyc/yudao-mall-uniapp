<template>
  <view class="page">
    <!-- 顶部导航栏 -->
    <view class="header">
      <view class="back-btn" @click="goBack">
        <text class="back-icon">←</text>
      </view>
      <text class="title">短信通知</text>
      <view class="placeholder"></view>
    </view>

    <!-- 主要内容区 -->
    <view class="content">
      <!-- 表单区域 -->
      <view class="form-group">
        <input
          class="input-field"
          v-model="nickname"
          placeholder="请输入你的昵称"
          type="text"
        />
      </view>
      <view class="form-group">
        <input
          class="input-field"
          v-model="phoneNumber"
          placeholder="请输入对方手机号"
          type="number"
          maxlength="11"
        />
      </view>
      <view class="form-group date-picker" @click="showDatePicker">
        <text class="date-text">{{ selectedDateTime || '选择日期时间' }}</text>
        <text class="arrow">></text>
      </view>

      <!-- 短信格式预览 -->
      <view class="sms-preview">
        <text class="preview-label">短信格式：</text>
        <text class="preview-content">有人给你写了一封信，验证码为：ABCDE，微信搜索「写一封信」输入验证码查看。</text>
      </view>
    </view>

    <!-- 底部区域 -->
    <view class="footer">
      <view class="price-info">
        <text>短信通知价格：5.2元一次</text>
      </view>
      <view class="send-btn" @click="sendNotification">
        <text>发送</text>
      </view>
    </view>

    <!-- 日期时间选择器 -->
    <uni-datetime-picker
      ref="dateTimePicker"
      type="datetime"
      :value="selectedDateTime"
      @change="onDateTimeChange"
      :clear-icon="false"
      v-model="selectedDateTime"
    />
  </view>
</template>

<script setup>
import { ref } from 'vue';

// 表单数据
const nickname = ref('');
const phoneNumber = ref('');
const selectedDateTime = ref('');
const dateTimePicker = ref(null);

// 返回上一页
const goBack = () => {
  uni.navigateBack();
};

// 显示日期时间选择器
const showDatePicker = () => {
  dateTimePicker.value.show();
};

// 日期时间变化处理
const onDateTimeChange = (value) => {
  selectedDateTime.value = value;
};

// 发送短信通知
const sendNotification = () => {
  if (!nickname.value.trim()) {
    uni.showToast({
      title: '请输入昵称',
      icon: 'none'
    });
    return;
  }

  if (!phoneNumber.value || phoneNumber.value.length !== 11) {
    uni.showToast({
      title: '请输入正确的手机号',
      icon: 'none'
    });
    return;
  }

  if (!selectedDateTime.value) {
    uni.showToast({
      title: '请选择日期时间',
      icon: 'none'
    });
    return;
  }

  // TODO: 实现发送短信通知的逻辑
  uni.showToast({
    title: '发送成功',
    icon: 'success'
  });
};
</script>

<style lang="scss" scoped>
.page {
  min-height: 100vh;
  background-color: #fff;
  display: flex;
  flex-direction: column;
}

.header {
  padding: 44px 20px 20px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  
  .back-btn {
    width: 40px;
    height: 40px;
    display: flex;
    align-items: center;
    justify-content: center;
    
    .back-icon {
      font-size: 24px;
    }
  }
  
  .title {
    font-size: 18px;
    font-weight: bold;
  }
  
  .placeholder {
    width: 40px;
  }
}

.content {
  flex: 1;
  padding: 20px;
}

.form-group {
  margin-bottom: 20px;
  
  .input-field {
    width: 100%;
    height: 50px;
    border: 1px solid #eee;
    border-radius: 25px;
    padding: 0 20px;
    font-size: 16px;
  }
}

.date-picker {
  border: 1px solid #eee;
  border-radius: 25px;
  height: 50px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 0 20px;
  
  .date-text {
    font-size: 16px;
    color: #333;
  }
  
  .arrow {
    color: #999;
  }
}

.sms-preview {
  margin-top: 30px;
  
  .preview-label {
    font-size: 14px;
    color: #999;
    margin-bottom: 10px;
    display: block;
  }
  
  .preview-content {
    font-size: 16px;
    line-height: 1.5;
    color: #333;
  }
}

.footer {
  padding: 20px;
  border-top: 1px solid #f5f5f5;
  
  .price-info {
    text-align: center;
    margin-bottom: 20px;
    
    text {
      color: #999;
      font-size: 14px;
    }
  }
  
  .send-btn {
    background-color: #00C853;
    border-radius: 25px;
    height: 50px;
    display: flex;
    align-items: center;
    justify-content: center;
    
    text {
      color: #fff;
      font-size: 16px;
      font-weight: bold;
    }
  }
}
</style>