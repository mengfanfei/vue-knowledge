<script setup lang="ts">

import ChartType from '@/components/ChartType.vue'
import { PieDataOptions, PieOption, getOptions } from '@/components/chartModules/PieChart/echarts.options'
import { onMounted, ref, watch } from 'vue'

const props = defineProps<{
  data: PieDataOptions
}>()

const options = ref<PieOption>()

const renderData = () => {
  if (props.data && props.data.dataArr) {
    options.value = getOptions(props.data)
  } else {
    options.value = {}
    console.log('props.data.dataArr is undefined')
  }
}

watch(()=> props.data, () => {
  renderData()
}, { deep: true })

onMounted(() => {
  renderData()
})

</script>

<template>
  <div style="width: 100%; height: 100%; position: relative;">
    <ChartType :options="options" />
  </div>
</template>

<style scoped>

</style>
