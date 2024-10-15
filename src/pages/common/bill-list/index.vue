<template>
  <z-paging ref="paging" v-model="dataList" empty-view-text="空空如也~~" @query="queryList">
    <!-- z-paging默认铺满全屏，此时页面所有view都应放在z-paging标签内，否则会被盖住 -->
    <!-- 需要固定在页面顶部的view请通过slot="top"插入，包括自定义的导航栏 -->
    <view v-for="(item, index) in dataList" :key="index" class="item" @click="handleGoToDeatil">
      <view>{{ item.title }}</view>
    </view>
  </z-paging>
</template>

<script setup lang="ts">
const dataList = ref<Record<string, any>[]>([]);
const paging = ref();

const queryList = (pageNo: number, pageSize: number) => {
  console.log(pageNo, pageSize);
  paging.value.complete([{ title: '测试账单' }]);
};

const handleGoToDeatil = () => {
  uni.navigateTo({ url: '/pages/common/bill-detail/index' });
};
</script>
