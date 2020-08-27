<template>
    <div>
        <h1>UK Energy Mix</h1>
        <display-chart :generationMix="generationMix"></display-chart>
    </div>
</template>

<script>
import DisplayChart from './components/DisplayChart.vue'

export default {
  name: 'app',
  data(){
    return {
      generationMix: []
      }
  },
  mounted(){
    this.fetchData()
  },
  methods:{
      fetchData(){
          fetch('https://api.carbonintensity.org.uk/generation')
          .then(resp => resp.json())
          .then(data => this.generationMix = this.formatForChart(data.data.generationmix))
      },
     
      formatForChart(objectList) {
        const newList = objectList.map((object)=>{
          return [object.fuel, object.perc]})
        newList.unshift(["Fuel", "Percentage"])
        return newList
      }
  },
  components: {
    'display-chart': DisplayChart
  }
      
}
</script>

<style>

</style>