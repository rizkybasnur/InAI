<script setup>
const props = defineProps({
  title: {
    type: String,
    default: ''
  },
  purple: {
    type: Boolean,
    default: false
  },
  useIcon: {
    type: Boolean,
    default: false
  },
  urlIcon: {
    type: String,
    default: ''
  },
  useSingleIcon: {
    type: Boolean,
    default: false
  },
  useTwoIcon: {
    type: Boolean,
    default: false
  },
  urlStart: {
    type: String,
    default: ''
  },
  urlEnd: {
    type: String,
    default: ''
  },
  style: {
    type: [Object, String],
    default: () => {
      return {}
    }
  },
  titleStyle: {
    type: [Object, String],
    default: () => {
      return {}
    }
  }
})

const useIconPath = (v) => {
  if (!props['url' + v]) return ''
  try {
    return new URL(`${props['url' + v]}`, import.meta.url).href
  } catch (error) {
    console.error('Error resolving icon path:', error)
    return ''
  }
}
</script>

<template>
  <button
    v-if="useSingleIcon"
    class="cursor-pointer bg-none radius-24 gray-60 border-gray-30 w-100 padding-button 100 d-flex item-center justify-center"
    :class="{ 'bg-brand-60 border-none ': purple }"
  >
    <img :src="useIconPath('Start')" style="margin-right: 8px" />
    <span class="text-sm-bold" :class="{ 'gray-0': purple }">{{ title }}</span>
  </button>

  <button
    v-if="useTwoIcon"
    class="cursor-pointer border-none radius-24 w-100 d-flex item-center justify-center bg-blue-60 gray-0 padding-button"
  >
    <img :src="useIconPath('Start')" class="mr-8" />
    <span class="text-md-bold">{{ title }}</span>
    <img :src="useIconPath('End')" style="margin-left: 8px" />
  </button>

  <button v-if="useIcon" class="cursor-pointer border-none bg-none">
    <img :src="useIconPath('Icon')" />
  </button>
</template>
