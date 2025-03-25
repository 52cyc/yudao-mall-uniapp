<template>
  <view class="page">
    <!-- 顶部标题栏 -->
    <view class="header">
      <text class="title">首页</text>
    </view>
    
    <!-- 主要内容区 -->
    <view class="content">
      <!-- 标语 -->
      <view class="slogan">
        <text class="slogan-text">想说的话</text>
        <text class="slogan-text">我帮你送达</text>
      </view>
      
      <!-- 功能按钮区 -->
      <view class="function-area">
        <!-- 写信按钮 -->
        <view class="write-letter-box">
          <view class="write-letter">
            <text class="write-letter-title">写一封信</text>
            <text class="write-letter-subtitle">悄悄送给TA</text>
            <view class="write-letter-btn" @click="startWriteLetter">
              <text>开始写信</text>
            </view>
          </view>
        </view>
        
        <!-- 右侧按钮组 -->
        <view class="right-buttons">
          <view class="verify-code" @click="verifyCode">
            <text>验证码收信</text>
          </view>
          <view class="personal-center" @click="goToPersonalCenter">
            <text>个人中心</text>
          </view>
        </view>
      </view>
      
      <!-- 广告区域 -->
      <view class="ad-area">
        <view class="ad-item">
          <!-- 广告内容 -->
        </view>
      </view>
    </view>

    <!-- 验证码弹窗 -->
    <uni-popup ref="popup" type="center">
      <view class="verify-popup">
        <view class="verify-title">验证码收信</view>
        <input 
          class="verify-input" 
          type="text" 
          v-model="verifyCodeInput"
          placeholder="请输入取件码"
          maxlength="5"
        />
        <view class="verify-btn" @click="submitVerifyCode">确定</view>
      </view>
    </uni-popup>
  </view>
</template>

<script setup>
import { onMounted, ref } from 'vue';
import { onLoad } from '@dcloudio/uni-app';
const popup = ref(null);

const verifyCodeInput = ref('');

onMounted(() => {
  console.log(popup.value); // 检查是否绑定成功
});

// 开始写信
const startWriteLetter = () => {
  uni.navigateTo({
    url: '/pages/index/write-letter'
  });
};

// 验证码收信
const verifyCode = () => {
  console.log('验证码收信');
  if (popup.value) {
    popup.value.open();
  } else {
    uni.showToast({
      title: '组件初始化失败',
      icon: 'none'
    });
  }
};

// 提交验证码
const submitVerifyCode = () => {
  if (!verifyCodeInput.value) {
    uni.showToast({
      title: '请输入验证码',
      icon: 'none'
    });
    return;
  }
  
  if (verifyCodeInput.value.length !== 5) {
    uni.showToast({
      title: '验证码格式错误',
      icon: 'none'
    });
    return;
  }
  
  // TODO: 调用验证码验证接口
  console.log('验证码:', verifyCodeInput.value);
  popup.value.close();
  verifyCodeInput.value = '';
  
  // 跳转到信件详情页
  uni.navigateTo({
    url: `/pages/index/letter-detail?code=${verifyCodeInput.value}`
  });
};

// 跳转到个人中心
const goToPersonalCenter = () => {
  uni.navigateTo({
    url: '/pages/index/personal-center'
  });
};

onLoad(() => {
  // 页面加载时的逻辑
});
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

.content {
  padding: 20px;
}

.slogan {
  margin-bottom: 30px;
  
  .slogan-text {
    display: block;
    font-size: 28px;
    font-weight: bold;
    line-height: 1.5;
  }
}

.function-area {
  display: flex;
  gap: 20px;
  margin-bottom: 30px;
}

.write-letter-box {
  flex: 1;
}

.write-letter {
  background-color: #00C853;
  border-radius: 20px;
  padding: 30px 20px;
  height: 200px;
  color: #fff;
  
  .write-letter-title {
    font-size: 24px;
    font-weight: bold;
    display: block;
    margin-bottom: 10px;
  }
  
  .write-letter-subtitle {
    font-size: 16px;
    opacity: 0.8;
    display: block;
    margin-bottom: 30px;
  }
  
  .write-letter-btn {
    background-color: #fff;
    border-radius: 25px;
    padding: 12px 30px;
    display: inline-block;
    
    text {
      color: #00C853;
      font-size: 16px;
      font-weight: bold;
    }
  }
}

.right-buttons {
  width: 150px;
  display: flex;
  flex-direction: column;
  gap: 20px;
  
  .verify-code, .personal-center {
    flex: 1;
    border-radius: 20px;
    display: flex;
    align-items: center;
    justify-content: center;
    font-size: 16px;
    font-weight: bold;
    color: #fff;
  }
  
  .verify-code {
    background-color: #FF4081;
  }
  
  .personal-center {
    background-color: #FFA000;
  }
}

.ad-area {
  margin-top: 20px;
  
  .ad-item {
    background-color: #f5f5f5;
    border-radius: 20px;
    height: 200px;
    // 广告样式
  }
}

.verify-popup {
  background-color: #fff;
  border-radius: 16px;
  width: 280px;
  padding: 24px;
  
  .verify-title {
    font-size: 18px;
    font-weight: bold;
    text-align: center;
    margin-bottom: 20px;
  }
  
  .verify-input {
    width: 100%;
    height: 44px;
    border: 1px solid #eee;
    border-radius: 8px;
    padding: 0 16px;
    font-size: 16px;
    margin-bottom: 20px;
  }
  
  .verify-btn {
    background-color: #00C853;
    color: #fff;
    height: 44px;
    line-height: 44px;
    text-align: center;
    border-radius: 8px;
    font-size: 16px;
    font-weight: bold;
  }
}
</style>
