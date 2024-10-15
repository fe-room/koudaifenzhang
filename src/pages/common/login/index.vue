<template>
  <view>
    <nav-bar title="登录">
      <view class="homt-icon-wrap" @click="handleNav">
        <up-icon v-if="isQuickLogin" color="#000000" bold name="home" size="24" />
        <up-icon v-else color="#000000" bold name="arrow-left" size="24" />
      </view>
    </nav-bar>
    <view class="login-form-wrap">
      <view class="title">
        欢迎使用口袋分账
      </view>
      <template v-if="isQuickLogin">
        <u-button text="手机号快捷登录" type="primary" shape="circle" @click="getCode" />
        <up-text type="info" text="其它登录方式" size="12" align="center" margin="15px 0 0 0" @click="isQuickLogin = false" />
      </template>
      <template v-else>
        <input v-model="tel" class="u-border-bottom" type="number" placeholder="请输入手机号">
        <view class="u-border-bottom my-40rpx flex">
          <input v-model="code" class="flex-1" type="number" placeholder="请输入验证码">
          <view>
            <u-code ref="uCodeRef" @change="codeChange" />
            <u-button :text="tips" type="primary" size="mini" @click="getCode" />
          </view>
        </view>
        <u-button type="primary" :disabled="!isSubmit" @tap="submit">
          登录
        </u-button>
      </template>
    </view>
  </view>
</template>

<script setup lang="ts">
import uCode from 'uview-plus/components/u-code/u-code.vue';
import { setToken } from '@/utils/auth';
import navBar from '@/components/page-nav/index.vue';

const tel = ref<string>('18502811111');
const code = ref<string>('1234');
const tips = ref<string>();
const uCodeRef = ref<InstanceType<typeof uCode> | null>(null);
const isQuickLogin = ref(true);
function codeChange(text: string) {
  tips.value = text;
}
const isSubmit = computed(() => (tel.value && code.value));
function getCode() {
  if (uCodeRef.value?.canGetCode) {
    // 模拟向后端请求验证码
    uni.showLoading({
      title: '正在获取验证码',
    });
    setTimeout(() => {
      uni.hideLoading();
      uni.$u.toast('验证码已发送');
      // 通知验证码组件内部开始倒计时
      uCodeRef.value?.start();
    }, 1000);
  }
  else {
    uni.$u.toast('倒计时结束后再发送');
  }
}
async function submit() {
  if (!uni.$u.test.mobile(Number(tel.value))) {
    uni.$u.toast('请输入正确的手机号');
    return;
  }
  if (!code.value) {
    uni.$u.toast('请输入验证码');
    return;
  }
  // 登录请求
  // const res = await userStore.login({ phone: tel.value, code: code.value }).catch(() => {
  //   uni.$u.toast('登录失败');
  // });
  // if (!res) return;
  setToken('1234567890');
  uni.reLaunch({ url: '/pages/tab/home/index' });
}

const goHome = () => {
  uni.reLaunch({
    url: '/pages/index/index',
  });
};

const handleNav = () => {
  if (isQuickLogin.value) {
    goHome();
  }
  else {
    isQuickLogin.value = true;
  }
};
</script>

<style lang="scss" scoped>
.login-form-wrap {
  @apply mt-175rpx mx-auto mb-0 w-600rpx;

  .title {
    @apply mb-100rpx text-40rpx text-center font-500;
  }

  input {
    @apply pb-6rpx mb-10rpx text-left;
  }

  .tips {
    @apply mt-8rpx mb-60rpx;

    color: $u-info;
  }

}

.homt-icon-wrap {
    position: absolute;
    top: 0;
    bottom: 0;
    left: 20rpx;
    display: flex;
    justify-content: center;
    align-items: center;
    margin: auto 0;
    width: 56rpx;
    height: 56rpx;
    font-size: 0;
    background: #fff;
    border-radius: 50%;

    .home-icon {
      width: 36rpx;
      height: 36rpx;
    }
  }
</style>
