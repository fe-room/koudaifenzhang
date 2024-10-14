<template>
  <z-paging ref="paging" v-model="dataList" empty-view-text="空空如也~~ 点击+号开始记账吧" @query="queryList">
    <!-- z-paging默认铺满全屏，此时页面所有view都应放在z-paging标签内，否则会被盖住 -->
    <!-- 需要固定在页面顶部的view请通过slot="top"插入，包括自定义的导航栏 -->
    <view v-for="(item, index) in dataList" :key="index" class="item">
      <view>111</view>
    </view>
  </z-paging>
</template>

<script setup lang="ts">
const dataList = ref([]);
const paging = ref();

const queryList = (pageNo: number, pageSize: number) => {
  console.log(pageNo, pageSize);
  paging.value.complete([{ title: 'one' }]);
};
</script>
