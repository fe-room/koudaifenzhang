<template>
  <up-popup v-model:show="show" :custom-style="styleObj" :round="10" closeable @close="handleClose">
    <view class="popup-box">
      <view class="text-center">
        <text class="font-size-4 font-500">
          新建账单
        </text>
      </view>
      <view class="pt-4">
        <view class="pb-4">
          <up-input
            v-model="billInfo.title"
            placeholder="账单名称"
          />
        </view>
        <up-subsection mode="subsection" :list="list" :current="current" />
      </view>
    </view>
    <view class="position-absolute bottom-20rpx left-60rpx right-60rpx">
      <up-button type="primary" text="确定" />
    </view>
  </up-popup>
</template>

<script lang="ts" setup>
const props = defineProps({
  open: {
    type: Boolean,
    default: false,
  },
});
const emit = defineEmits(['close']);
const show = ref(false);
const styleObj = ref();
const billInfo = ref({
  title: '',
  type: '',
});
const list = ref(['单人账本', '多人AA']);
const current = ref(0);
watch(
  () => props.open,
  (newValue) => {
    show.value = newValue;
  },
);
onMounted(() => {
  const { windowHeight } = uni.getSystemInfoSync();
  styleObj.value = { height: `${windowHeight * 0.8}px` };
});

const handleClose = () => {
  emit('close');
};
</script>

<style lang=scss scoped>
.popup-box {
   padding: 60rpx;
}
</style>
