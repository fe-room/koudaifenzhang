<template>
  <view class="bill">
    <view class="bill-title row flex justify-between">
      <text class="font-size-4 font-500">
        账单标题
      </text>
      <image
        src="@/static/images/share.png"
        mode="scaleToFill"
        class="h-40rpx w-40rpx"
      />
    </view>
    <view class="bill-info">
      <view class="row flex justify-between flex-items-center">
        <text class="font-size-4 font-500">
          合计
        </text>
        <text class="font-size-6 font-500">
          ￥2000
        </text>
      </view>
      <view class="pt-6">
        <view class="row flex justify-between flex-items-center">
          <text class="clor-gray font-size-4">
            分摊
          </text>
          <text class="clor-gray font-size-4">
            4人
          </text>
        </view>
        <view class="pt-4">
          <view class="row flex justify-between flex-items-center">
            <up-avatar-group
              :urls="urls"
              size="35"
            />
            <image
              src="@/static/images/invite.png"
              mode="scaleToFill"
              class="h-64rpx w-64rpx"
            />
          </view>

          <view class="mt-4">
            <up-button type="primary" text="分摊" />
          </view>
        </view>
      </view>
    </view>
  </view>
</template>

<script lang="ts" setup>
const urls = reactive([
  'ttps://uview-plus.jiangruyi.com/uview-plus/album/1.jpg',
  'https://uview-plus.jiangruyi.com/uview-plus/album/2.jpg',
  'https://uview-plus.jiangruyi.com/uview-plus/album/3.jpg',
  'https://uview-plus.jiangruyi.com/uview-plus/album/4.jpg',
  'https://uview-plus.jiangruyi.com/huview-plus/album/7.jpg',
  'https://uview-plus.jiangruyi.com/uview-plus/album/6.jpg',
  'https://uview-plus.jiangruyi.com/uview-plus/album/5.jpg',
]);
</script>

<style lang="scss" scoped>
 .bill {
    padding: 60rpx;
    width: 500rpx;
    height: 500rpx;
    background: #FFF;
    border-radius: 60rpx;

    &-title {
        padding-bottom: 40rpx;
        border-bottom: 4rpx solid #F2F2F2;
    }

    &-info {
        padding-top: 40rpx;
    }
 }
</style>
