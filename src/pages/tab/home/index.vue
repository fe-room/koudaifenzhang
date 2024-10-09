<template>
  <view class="flex flex-col items-center justify-center">
    <image
      class="add-btn h-80rpx w-80rpx"
      src="@/static/tabbar/add.png"
    />
    <!-- #ifdef MP-WEIXIN -->
    <!-- 隐私协议组件 -->
    <agree-privacy v-model="showAgreePrivacy" :disable-check-privacy="false" @agree="handleAgree" />
    <!-- #endif -->
  </view>
</template>

<script setup lang="ts">
import { useUserStore } from '@/store';

const title = ref<string>();
title.value = import.meta.env.VITE_APP_TITLE;

const store = useUserStore();
console.log('store.user_name', store.user_name);

const showAgreePrivacy = ref(false);
// 同意隐私协议
function handleAgree() {
  console.log('同意隐私政策');
}
</script>

<style scoped lang="scss">
.add-btn {
   position: absolute;
   right: 100rpx;
   bottom: 100rpx;
}
</style>
