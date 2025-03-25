<template>
  <view class="page">
    <!-- 顶部导航栏 -->
    <view class="header">
      <view class="back-btn" @click="goBack">
        <text class="back-icon">←</text>
      </view>
      <text class="title">写一封信</text>
      <view class="placeholder"></view>
    </view>

    <!-- 主要内容区 -->
    <view class="content">
      <textarea
        class="letter-input"
        v-model="letterContent"
        placeholder="请输入要添加的文字"
        :maxlength="1000"
        @input="onInput"
      />
    </view>

    <!-- 底部区域 -->
    <view class="footer">
      <view class="counter">
        <text>{{ contentLength }} / 1000</text>
      </view>
      <view class="tips">
        <text class="tips-text">Tips：该内容发布后可能会被隐藏而不予展示</text>
      </view>
      <view class="send-btn" @click="sendLetter">
        <text>发送</text>
      </view>
    </view>

    <!-- 成功弹窗 -->
    <uni-popup type="center" v-if="successState" :mask="true">
      <view class="success-popup">
        <view class="success-title">创建成功</view>
        <view class="verification-code">
          <text class="code-label">你的验证码</text>
          <text class="code-value">VPSZO</text>
        </view>
        <view class="tips-text">tips：写的信可以在个人中心查看</view>
        <view class="action-buttons">
          <view class="share-btn" @click="handleShare">分享一下</view>
          <view class="notify-btn" @click="handleNotify">短信通知</view>
        </view>
      </view>
    </uni-popup>


  </view>
</template>

<script setup>
import { ref } from 'vue';

// 信件内容
const letterContent = ref('');
const contentLength = ref(0);
const successPopup = ref(null);
const successState = ref(false);

// 监听输入
const onInput = () => {
  contentLength.value = letterContent.value.length;
};

// 返回上一页
const goBack = () => {
  uni.navigateBack();
};

// 发送信件
const sendLetter = () => {
  if (!letterContent.value.trim()) {
    uni.showToast({
      title: '请输入信件内容',
      icon: 'none'
    });
    return;
  }

  // TODO: 实现发送信件的逻辑
  successState.value = true;
  
};

// 分享处理
const handleShare = () => {
  // TODO: 实现分享功能
  uni.showToast({
    title: '分享功能开发中',
    icon: 'none'
  });
};

// 短信通知处理
const handleNotify = () => {
  // 关闭成功弹窗
  successState.value = false;
  // 跳转到短信通知页面
  uni.navigateTo({
    url: '/pages/index/sms-notify?code=VPSZO'
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
  display: flex;
  flex-direction: column;
  
  .letter-input {
    width: 100%;
    height: 300px;
    font-size: 16px;
    line-height: 1.5;
    padding: 10px;
    border: 1px solid #eee;
    border-radius: 8px;
  }
}



.footer {
  padding: 20px;
  border-top: 1px solid #f5f5f5;
  
  .counter {
    text-align: right;
    margin-bottom: 10px;
    
    text {
      color: #999;
      font-size: 14px;
    }
  }
  
  .tips {
    margin-bottom: 20px;
    
    .tips-text {
      color: #999;
      font-size: 12px;
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



.success-popup,
.notify-popup {
  background-color: #fff;
  border-radius: 16px;
  padding: 30px;
  width: 320px;
  text-align: center;

  .success-title,
  .notify-title {
    font-size: 18px;
    font-weight: bold;
    margin-bottom: 20px;
  }

  .verification-code {
    margin: 20px 0;
    display: flex;
    flex-direction: column;
    align-items: center;

    .code-label {
      font-size: 14px;
      color: #999;
      margin-bottom: 10px;
    }

    .code-value {
      font-size: 32px;
      font-weight: bold;
      color: #333;
    }
  }

  .tips-text {
    font-size: 12px;
    color: #999;
    margin-bottom: 20px;
  }

  .action-buttons {
    display: flex;
    gap: 10px;

    .share-btn,
    .notify-btn {
      flex: 1;
      height: 40px;
      display: flex;
      align-items: center;
      justify-content: center;
      border-radius: 20px;
      font-size: 14px;
      font-weight: bold;
    }

    .share-btn {
      border: 1px solid #00C853;
      color: #00C853;
    }

    .notify-btn {
      background-color: #00C853;
      color: #fff;
    }
  }
  
  .notify-form {
    .input-field {
      width: 100%;
      height: 40px;
      border: 1px solid #eee;
      border-radius: 20px;
      padding: 0 15px;
      font-size: 14px;
      margin-bottom: 15px;
    }

    .date-picker {
      border: 1px solid #eee;
      border-radius: 20px;
      height: 40px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      padding: 0 15px;
      margin-bottom: 15px;
      
      .date-text {
        font-size: 14px;
        color: #333;
      }
      
      .arrow {
        color: #999;
      }
    }

    .sms-preview {
      text-align: left;
      margin-bottom: 20px;
      
      .preview-label {
        font-size: 14px;
        color: #333;
        margin-bottom: 5px;
        display: block;
      }
      
      .preview-content {
        font-size: 12px;
        color: #666;
        line-height: 1.5;
      }
    }
  }

  .notify-footer {
    .price-info {
      margin-bottom: 15px;
      
      text {
        font-size: 14px;
        color: #666;
      }
    }

    .notify-btn {
      background-color: #00C853;
      border-radius: 20px;
      height: 40px;
      display: flex;
      align-items: center;
      justify-content: center;
      
      text {
        color: #fff;
        font-size: 14px;
        font-weight: bold;
      }
    }
  }
}


</style>