<template>
  <view
    class="nav-bar"
    :style="{
      height: justStatusBar
        ? `${statusBarHeight}px`
        : `${statusBarHeight + barHeight}px`,
    }"
  >
    <view class="nav-wrap" :class="{ relative }" :style="{ background }">
      <view :style="{ height: `${statusBarHeight}px` }" />
      <view :style="{ height: `${barHeight}px` }" class="bar-height">
        <slot />
        <text class="title" :style="{ color: titleColor }">
          {{ title }}
        </text>
      </view>
    </view>
  </view>
</template>

<script setup lang="ts">
defineProps({
  justStatusBar: {
    type: Boolean,
    default: false,
  },
  title: {
    // 标题
    type: String,
    default: '',
  },
  background: {
    // 背景样色
    type: String,
    default: 'transparent',
  },
  relative: {
    // 是否固定头部
    type: Boolean,
    default: false,
  },
  titleColor: {
    type: String,
    default: '#000',
  },
});

const barHeight = ref(0);
const statusBarHeight = ref(0);
onMounted(() => {
  uni.getSystemInfo({
    // 获取头部高度
    success: (res: any) => {
      barHeight.value = res.system.includes('iOS') ? 44 : 48; // 如果是ios高为44，安卓为48
      statusBarHeight.value = res.statusBarHeight;
    },
    fail(err) {
      console.log(err);
    },
  });
});
</script>

<style lang="scss" scoped>
.nav-bar {
  position: fixed;
  top: 0;
  z-index: 99;
  width: 100%;
  color: #fff;
  background: rgb(255 255 255 / 75%);

  .nav-wrap {
    position: fixed;
    width: 100%;
  }

  .relative {
    position: relative;
  }

  .bar-height {
    position: relative;
    display: flex;
    justify-content: center;
    align-items: center;

    .title {
      font-weight: bold;
    }
  }
}
</style>
