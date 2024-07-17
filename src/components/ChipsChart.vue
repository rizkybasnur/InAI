<script setup>
defineProps({
  text: {
    type: String,
    default: ''
  },
  type: {
    type: String,
    default: ''
  }
})
</script>

<template>
  <div
    v-if="text !== ''"
    class="text-xs-semibold radius-24 padding-chip d-flex item-center gap-4"
    :class="{
      'success-50 bg-success-5': type === 'success',
      'gray-60 bg-gray-5': type === 'normal',
      'gray-0 bg-success-80': type === 'successBold',
      'gray-0 bg-failed': type === 'failed'
    }"
  >
    <!-- 3 if for 3 conditions the icon to be showed -->
    <span v-if="type === 'success'">
      <img src="@/assets/icon/TrendUp.png" width="12" height="12" />
    </span>
    <span v-if="type === 'successBold'">
      <img src="@/assets/icon/TrendUpWhite.png" width="12" height="12" />
    </span>
    <span v-if="type === 'failed'">
      <img src="@/assets/icon/TrendUpWhite.png" width="12" height="12" />
    </span>
    <!-- text for the title of the chips -->
    {{ text }}
  </div>
</template>
