<template>
    <GChart
    type="PieChart"
    :data="generationMix"
    :options="chartOptions"
  />
</template>

<script>
import { GChart } from 'vue-google-charts'

export default {
  components: {
    GChart
  },
  props:['generationMix']
}
</script>

<style>

</style>
