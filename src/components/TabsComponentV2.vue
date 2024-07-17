<script setup>
import { ref } from 'vue'

const props = defineProps({
  data: {
    type: Array,
    required: true
  },
  outlined: {
    type: Boolean,
    default: true
  }
})

const svgColor = ref('#4f46e5')

const toggleCountry = (id) => {
  props.data.forEach((v) => {
    v.active = v.id === id
  })
  if (id === 0) {
    svgColor.value = '#4f46e5'
  } else {
    svgColor.value = '#475569'
  }
}
</script>

<template>
  <div class="d-flex bg-grey-2 p-4 radius-24 justify-between;">
    <button
      v-for="(item, index) in data"
      :key="index"
      class="cursor-pointer p-tab radius-24 border-none item-center d-flex text-sm-bold"
      :class="!item.active ? 'bg-none gray-60' : 'bg-white purple'"
      @click="toggleCountry(item.id)"
    >
      {{ item.name }}
    </button>
  </div>
</template>
