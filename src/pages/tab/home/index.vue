<template>
  <view class="flex flex-col items-center justify-center">
    <z-paging ref="paging" v-model="dataList" empty-view-text="空空如也~~ 点击+号开始记账吧" @query="queryList">
      <!-- z-paging默认铺满全屏，此时页面所有view都应放在z-paging标签内，否则会被盖住 -->
      <!-- 需要固定在页面顶部的view请通过slot="top"插入，包括自定义的导航栏 -->
      <view v-for="(item, index) in dataList" :key="index" class="item">
        <view class="item-title">
          {{ item.title }}
        </view>
      </view>
    </z-paging>
    <image
      class="add-btn h-80rpx w-80rpx"
      src="@/static/tabbar/add.png"
      @click="handleAddBill"
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
const paging = ref();
const dataList = ref([]);

title.value = import.meta.env.VITE_APP_TITLE;

const store = useUserStore();
console.log('store.user_name', store.user_name);

const showAgreePrivacy = ref(false);
// 同意隐私协议
function handleAgree() {
  console.log('同意隐私政策');
}
const queryList = (pageNo: number, pageSize: number) => {
  console.log(pageNo, pageSize);
  paging.value.complete([]);
};

const handleAddBill = () => {
  uni.navigateTo({ url: '/pages/common/create-bill/index' });
};
</script>

<style scoped lang="scss">
.add-btn {
   position: absolute;
   right: 100rpx;
   bottom: 100rpx;
}
</style>
