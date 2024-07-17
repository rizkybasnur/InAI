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

// default color of the globe svg
const svgColor = ref('#4f46e5')

// dynamically change the globe svg color based on the active condition
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
  <div class="mb-16 d-flex" :class="outlined ? 'justify-between' : 'gap-8'">
    <button
      v-for="(item, index) in data"
      :key="index"
      class="cursor-pointer padding-tab radius-24 bg-none item-center d-flex cardTabBig"
      :class="
        !item.active
          ? 'border-none grey-60'
          : outlined
            ? 'border-tab-active purple'
            : 'border-none bg-grey-1 purple'
      "
      @click="toggleCountry(item.id)"
    >
      <div v-if="item.icon" style="margin-right: 4px">
        <!-- svg only for the globe so it can change color dynamically -->
        <svg
          v-if="item.id === 0"
          :style="{ fill: svgColor }"
          width="16"
          height="16"
          viewBox="0 0 14 14"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M7 0.25C5.66498 0.25 4.35994 0.645881 3.2499 1.38758C2.13987 2.12928 1.27471 3.18349 0.763816 4.41689C0.252925 5.65029 0.119252 7.00749 0.379702 8.31686C0.640153 9.62623 1.28303 10.829 2.22703 11.773C3.17104 12.717 4.37377 13.3598 5.68314 13.6203C6.99252 13.8808 8.34971 13.7471 9.58312 13.2362C10.8165 12.7253 11.8707 11.8601 12.6124 10.7501C13.3541 9.64007 13.75 8.33502 13.75 7C13.748 5.2104 13.0362 3.49466 11.7708 2.22922C10.5053 0.963781 8.78961 0.251985 7 0.25ZM7 11.9375C6.44737 11.2907 6.01569 10.5497 5.72563 9.75H8.27688C8.11181 10.2022 7.90246 10.6371 7.65188 11.0481C7.45906 11.3618 7.24105 11.6592 7 11.9375ZM5.34438 8.25C5.22063 7.42126 5.22063 6.57874 5.34438 5.75H8.65688C8.78063 6.57874 8.78063 7.42126 8.65688 8.25H5.34438ZM1.75 7C1.74998 6.57873 1.80098 6.15901 1.90188 5.75H3.82813C3.72396 6.58008 3.72396 7.41992 3.82813 8.25H1.90188C1.80098 7.84099 1.74998 7.42127 1.75 7ZM7 2.0625C7.55264 2.70928 7.98431 3.45026 8.27438 4.25H5.72438C5.88945 3.79776 6.0988 3.36294 6.34938 2.95187C6.54179 2.63827 6.75938 2.34084 7 2.0625ZM10.1706 5.75H12.0969C12.2994 6.57103 12.2994 7.42897 12.0969 8.25H10.1719C10.276 7.41992 10.276 6.58008 10.1719 5.75H10.1706ZM11.4688 4.25H9.85688C9.63166 3.49399 9.30583 2.77168 8.88813 2.1025C9.95946 2.51839 10.8659 3.27235 11.47 4.25H11.4688ZM5.11188 2.1025C4.69418 2.77168 4.36835 3.49399 4.14313 4.25H2.53C3.13408 3.27235 4.04054 2.51839 5.11188 2.1025ZM2.53 9.75H4.14313C4.36835 10.506 4.69418 11.2283 5.11188 11.8975C4.04054 11.4816 3.13408 10.7277 2.53 9.75ZM8.88813 11.8975C9.30583 11.2283 9.63166 10.506 9.85688 9.75H11.47C10.8659 10.7277 9.95946 11.4816 8.88813 11.8975Z"
          />
        </svg>

        <!-- img for the flags that doesnt need the color to be changed  -->
        <img
          v-else
          :src="`src/assets/icon/${item.icon}`"
          :style="{ fill: svgColor }"
          width="16"
          height="16"
        />
      </div>
      <span class="text-sm-semibold">{{ item.name }}</span>
    </button>
  </div>
</template>
