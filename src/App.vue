<script setup>
import { reactive, ref, watch, computed } from 'vue'
import TabsComponent from './components/TabsComponent.vue'
import ButtonComponent from './components/ButtonComponent.vue'
import CardComponent from './components/CardComponent.vue'
import ChipsChart from '@/components/ChipsChart.vue'

// <!-- start: populate data for portfolio section -->
const tagData = reactive([
  { id: 0, name: 'All', active: true },
  { id: 1, name: 'Realised gains', active: false },
  { id: 2, name: 'Unrealised gains', active: false }
])

const portfolio = ref([
  { name: 'All', dollar: '+$401,321', percent: '+0.5%' },
  { name: 'Realised gains', dollar: '$814,603', percent: '-1.1%' },
  { name: 'Unrealised gains', dollar: '+$3,285,372', percent: '+1.1%' }
])

const all = ref([
  { name: 'All', dollar: '+$401,321', percent: '+0.5%' },
  { name: 'Realised gains', dollar: '-$814,603', percent: '-1.1%' },
  { name: 'Unrealised gains', dollar: '+$3,285,372', percent: '+1.1%' }
])

const realised = ref([
  { name: 'All', dollar: '$0', percent: '' },
  { name: 'Realised gains', dollar: '+$500,000', percent: '+0.7%' },
  { name: 'Unrealised gains', dollar: '+$1,219,000', percent: '+1.7%' }
])

const unrealised = ref([
  { name: 'All', dollar: '+$401,321', percent: '+0.5%' },
  { name: 'Realised gains', dollar: '-$314,603', percent: '-0.4%' },
  { name: 'Unrealised gains', dollar: '+$2,066,372', percent: '+2.9%' }
])

// note: filtering only the active object
const active = computed(() => tagData.filter((e) => e.active))

// note:checking value to determine the condition of the chips
const checkValue = (v) => {
  if (v.slice(0, 1) === '+') return 'successBold'
  if (v.slice(0, 1) === '-') return 'failed'
}

// note: looking the change of data to assign different value to dummy to show
watch(tagData, () => {
  if (active.value[0].id === 0) portfolio.value = all.value
  if (active.value[0].id === 1) portfolio.value = realised.value
  if (active.value[0].id === 2) portfolio.value = unrealised.value
})
// <!-- end: populate data for portfolio section -->

// note: value for ai suggestion
const suggestions = reactive([
  'Listed shares balances per month?',
  'Liquid assets per account?',
  'What are current portfolio risks?'
])

// note: value for tab data
const countries = reactive([
  { id: 0, name: 'All', icon: 'Global.svg', active: true },
  { id: 1, name: 'Australia', icon: 'Australia.png', active: false },
  { id: 2, name: 'USA', icon: 'Usa.png', active: false },
  { id: 3, name: 'Europe', icon: 'Europe.png', active: false }
])
</script>

<template>
  <header>
    <!-- start: section navigation -->
    <nav style="display: flex; justify-content: space-between; align-items: center">
      <img
        class="cursor-pointer"
        alt="Avatar"
        src="@/assets/icon/Avatar.png"
        width="40"
        height="40"
      />
      <img class="cursor-pointer" alt="InAI" src="@/assets/icon/InAI.png" width="38" />
      <img
        class="display-non-big cursor-pointer"
        alt="Avatar"
        src="@/assets/icon/Button Icon (1).png"
        width="40"
        height="40"
      />
    </nav>
    <!-- start: section navigation -->
  </header>

  <main>
    <!-- start: section net assets and gross income -->
    <section class="wrapper">
      <div
        style="margin: 16px 0; display: flex; align-items: center; justify-content: space-between"
      >
        <div class="heading-xs-extrabold">Portfolio Dashboard</div>

        <div class="button-search">
          <ButtonComponent useIcon urlIcon="../assets/icon/Magnify.png" />
        </div>
        <div class="inputSearch w-50">
          <input type="text" placeholder="Search" class="radius-24 p-16 border-gray-30 w-100" />
        </div>
      </div>

      <div style="margin-bottom: 16px">
        <ButtonComponent
          useTwoIcon
          urlStart="../assets/icon/MagicWand.png"
          title="Ask AI assistant"
          urlEnd="../assets/icon/ArrowRight.png"
        />
        <div class="typewriter">
          <h6>E.g.: How much liquid assets I have in US account</h6>
        </div>
      </div>

      <div class="flex-big">
        <div class="container-big">
          <TabsComponent :data="countries" />

          <CardComponent :data="countries" />
        </div>

        <CardComponent class="card-outline-big" white no-chip />
      </div>
    </section>
    <!-- end: section net assets and gross income -->

    <!-- start: section button asset and entity -->
    <section
      class="button-add"
      style="margin: 24px 0; display: flex; justify-content: space-between; gap: 8px"
    >
      <ButtonComponent
        useSingleIcon
        urlStart="../assets/icon/HandCoins.png"
        purple
        title="Add new asset"
      />
      <ButtonComponent
        useSingleIcon
        urlStart="../assets/icon/Buildings.png"
        title="Add new entity"
      />
    </section>
    <!-- end: section button asset and entity -->

    <!-- start: section portfolio and ai suggestion -->
    <section class="flex-big">
      <div
        class="portfolioBig"
        style="display: flex; flex-direction: column; gap: 16px; margin-bottom: 16px"
      >
        <div class="text-lg-bold grey-60">Portfolio performance</div>
        <TabsComponent :data="tagData" :outlined="false" />

        <div
          v-for="(d, i) in portfolio"
          :key="i"
          style="padding: 26px 8px"
          class="d-flex justify-between"
          :style="portfolio.length === i + 1 ? '' : 'border-bottom: 1px #e2e8f0 solid;'"
        >
          <div class="text-sm-semibold">{{ d.name }}</div>
          <div style="display: flex; gap: 4px">
            <div class="text-sm-bold">{{ d.dollar }}</div>
            <ChipsChart :type="checkValue(d.percent)" :text="d.percent" />
          </div>
        </div>
      </div>

      <CardComponent class="card-outline-small" white no-chip />

      <div class="aiBig">
        <div class="text-md-bold m-16-big">AI suggested queries</div>
        <div>
          <button
            v-for="(s, i) in suggestions"
            :key="i"
            class="cursor-pointer text-sm-bold gray-60 radius-24 w-100 mb-16 item-center padding-suggestion border-suggestion bg-none d-flex gap-8"
          >
            <img src="@/assets/icon/MagicWandBlack.png" width="20" height="20" />
            {{ s }}
          </button>
          <div class="display-non-big" style="width: 100%; border-bottom: 1px solid #cbd5e1"></div>
        </div>
      </div>
    </section>
    <!-- end: section portfolio and ai suggestion -->

    <!-- start: section button customize and widget -->
    <section
      class="padding-none"
      style="margin-top: 16px; display: flex; justify-content: center; gap: 8px; padding: 0 24px"
    >
      <ButtonComponent
        useSingleIcon
        urlStart="../assets/icon/SlidersHorizontal.png"
        title="Customise"
      />
      <ButtonComponent
        useSingleIcon
        urlStart="../assets/icon/CloudArrowUp.png"
        title="Add Widget"
      />
    </section>
    <!-- start: section button customize and widget -->
  </main>
</template>
