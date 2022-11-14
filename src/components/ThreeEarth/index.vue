<template>
  <div ref="chartRef"></div>
</template>

<script setup lang="ts">
import data from './data.json'
import { onMounted, ref, watch } from 'vue'

import World from './code/world/Word'

const chartRef = ref<HTMLElement>()
let threeClassInstance: World

onMounted(() => {
  const dom: HTMLElement | undefined = chartRef.value
  if (dom) {
    threeClassInstance = new World({
      dom: dom,
      data,
      width: 800,
      height: 800,
    })
  }
})
const updateData = (data: any) => {
  try {
    threeClassInstance.updateData(data)
  } catch (error) {
    console.log(error)
  }
}

watch(
  () => data,
  (newData: any) => {
    updateData(newData)
  },
  {
    deep: false,
  },
)
</script>
