<script setup>
import TabsComponentV2 from '@/components/TabsComponentV2.vue'
import { reactive, ref, watch, computed } from 'vue'
import ChipsChart from './ChipsChart.vue'

const props = defineProps({
  white: {
    type: Boolean,
    default: false
  },
  noChip: {
    type: Boolean,
    default: false
  },
  data: {
    type: Array,
    default: () => {
      return []
    }
  }
})
// <!-- start: populate data for net assets section -->
// note: data come from props is data that used to determined the object active or not
// note: filtering only the active object
const active = computed(() => props.data.filter((e) => e.active))

// note: looking the change of data to assign different value to dummy to show
watch(props.data, () => {
  if (active.value[0].id === 0) dummy.value = dummyAll.value
  if (active.value[0].id === 1) dummy.value = dummyAus.value
  if (active.value[0].id === 2) dummy.value = dummyUsa.value
  if (active.value[0].id === 3) dummy.value = dummyEurope.value
})

let dummy = ref({
  total: '$74,769,618',
  percentage: '+0.1%',
  gross: '$78,789,618',
  liabilities: '$4,020,000'
})

let dummyAll = ref({
  total: '$74,asdasd,618',
  percentage: '+0.1%',
  gross: '$78,789,618',
  liabilities: '$4,020,000'
})

let dummyAus = ref({
  total: '$102,769,618',
  percentage: '2.2%',
  gross: '$105,789,618',
  liabilities: '$3,020,000'
})

let dummyUsa = ref({
  total: '$20,769,618',
  percentage: '+1.1%',
  gross: '$24,789,618',
  liabilities: '$4,020,000'
})

let dummyEurope = ref({
  total: '$15,769,618',
  percentage: '+0.21%',
  gross: '$18,789,618',
  liabilities: '$3,020,000'
})
// <!-- end: populate data for net assets section -->

// <!-- start: populate data for gross income section -->
const dataTab = reactive([
  { id: 0, name: 'Day', active: true },
  { id: 1, name: 'Month', active: false },
  { id: 2, name: 'Quarter', active: false },
  { id: 3, name: 'FY 2024', active: false }
])

// note: filtering only the active object
const gross = computed(() => dataTab.filter((e) => e.active))

// note: looking the change of data to assign different value to dummy to show
watch(dataTab, () => {
  if (gross.value[0].id === 0) dummy2.value = dummy2All.value
  if (gross.value[0].id === 1) dummy2.value = dummy2Aus.value
  if (gross.value[0].id === 2) dummy2.value = dummy2Usa.value
  if (gross.value[0].id === 3) dummy2.value = dummy2Europe.value
})

let dummy2 = ref({
  total: '$64,769,618',
  percentage: '+0.3%',
  gross: '$78,789,618',
  liabilities: '$10,020,000'
})

let dummy2All = ref({
  total: '$99,769,618',
  percentage: '+0.05%',
  gross: '$102,789,618',
  liabilities: '$3,020,000'
})

let dummy2Aus = ref({
  total: '$123,769,618',
  percentage: '+0.7%',
  gross: '$125,789,453',
  liabilities: '$2,020,000'
})

let dummy2Usa = ref({
  total: '$52,934,618',
  percentage: '+0.2%',
  gross: '$54,789,123',
  liabilities: '$2,020,000'
})

let dummy2Europe = ref({
  total: '$86,893,618',
  percentage: '+0.1%',
  gross: '$90,592,618',
  liabilities: '$4,020,000'
})
// <!-- end: populate data for gross income section -->
</script>

<template>
  <div
    style=""
    class="p-16 radius-24 d-flex flex-column gap-12"
    :class="white ? 'blue-60 bg-none border-card' : 'gray-0 background-color bg-purple-30'"
  >
    <div class="d-flex justify-between">
      <div :class="!white ? 'card-title' : 'text-lg-bold'">
        {{ !white ? 'Net assets' : 'Gross  income' }}
      </div>
      <img
        class="cursor-pointer"
        src="@/assets/icon/DotsThreeOutlineVertical.png"
        width="20"
        height="20"
      />
    </div>
    <div class="d-flex justify-between item-center">
      <div>
        <div class="heading-sm-bold mb-8">{{ !white ? dummy?.total : dummy2.total }}</div>
        <div class="d-flex gap-8">
          <ChipsChart type="success" :text="!white ? dummy?.percentage : dummy2.percentage" />
          <span v-if="white">vs</span>
          <ChipsChart type="normal" text="last day" />
        </div>
      </div>
      <img v-if="!white" src="@/assets/icon/Icon Container (1).png" width="48" height="48" />
      <img v-if="white" src="@/assets/icon/Icon Container.png" width="48" height="48" />
    </div>
    <div>
      <div>
        <span class="card-text">{{ white ? 'Less expenses:' : 'Gross assets:' }}</span>
        <span class="card-text-bold" :class="{ 'destructive-90': white }">
          {{ !white ? dummy?.gross : dummy2.gross }}
        </span>
      </div>
      <div>
        <span class="card-text">Net income:</span>
        <span class="card-text-bold" :class="{ ' destructive-30': !white }">
          {{ !white ? dummy.liabilities : dummy2.liabilities }}
        </span>
      </div>
    </div>

    <div v-if="white">
      <TabsComponentV2 :data="dataTab" />
    </div>
  </div>
</template>
