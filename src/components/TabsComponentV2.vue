<script setup>
defineProps({
  data: {
    type: Array,
    required: true
  },
  outlined: {
    type: Boolean,
    default: true
  }
})
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
