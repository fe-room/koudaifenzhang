<template>
  <view class="flex flex-col p-50rpx">
    <view class="row flex justify-between">
      <text class="row-header">
        最近账单
      </text>
      <text class="row-more" @click="handleGotoList">
        更多
      </text>
    </view>
    <scroll-view :scroll-x="true" class="row-container pt-30rpx">
      <view class="row book-card-container-wrap flex">
        <BillItem v-for="(bill, index) in billList" :key="index" class="mr-20rpx" v-bind="bill" />
      </view>
    </scroll-view>
    <image
      class="add-btn h-80rpx w-80rpx"
      src="@/static/tabbar/add.png"
      @click="handleAddBill"
    />
    <!-- #ifdef MP-WEIXIN -->
    <!-- 隐私协议组件 -->
    <agree-privacy v-model="showAgreePrivacy" :disable-check-privacy="false" @agree="handleAgree" />
    <!-- #endif -->
    <CreatePopup :open="open" @close="handleClose" />
  </view>
</template>

<script setup lang="ts">
import CreatePopup from './components/create-popup/index.vue';
import BillItem from './components/bill-item/index.vue';
import { useUserStore } from '@/store';

const title = ref<string>();
const open = ref(false);
const billList = ref<any[]>([1, 2, 3, 4, 5]);

title.value = import.meta.env.VITE_APP_TITLE;

const store = useUserStore();
console.log('store.user_name', store.user_name);

const showAgreePrivacy = ref(false);
// 同意隐私协议
function handleAgree() {
  console.log('同意隐私政策');
}

const handleAddBill = () => {
  // uni.navigateTo({ url: '/pages/common/create-bill/index' });
  open.value = true;
};
const handleClose = (val: any) => {
  open.value = val;
};
const handleGotoList = () => {
  uni.navigateTo({ url: '/pages/common/bill-list/index' });
};
</script>

<style scoped lang="scss">
.add-btn {
   position: fixed;
   right: 100rpx;
   bottom: 100rpx;
}

.row-header {
  font-size: 32rpx;
  font-weight: 500;
}

.row-more {
  color: gray;
}

.row-container {
  display: flex;
  overflow: hidden;
  white-space: nowrap;
  flex-direction: row;
}
</style>
