<template>
    <div>
        <h1>UK Energy Mix</h1>
        <input type="date" v-model="dateFrom">
        <input type="date" v-model="dateTo">
        <button v-on:click="filterByDate" >Press Me</button>
        <display-chart :generationMix="generationMix"></display-chart>
    </div>
</template>

<script>
import DisplayChart from './components/DisplayChart.vue'

export default {
  name: 'app',
  data(){
    return {
      generationMix: [],
      dateFrom: "",
      dateTo: "",
      }
  },
  mounted(){
    this.fetchData("")
  },
  methods:{
      fetchData(filterDate){
          fetch(`https://api.carbonintensity.org.uk/generation${filterDate}`)
          .then(resp => resp.json())
          .then(data => this.generationMix = this.formatForChart(data.data.generationmix))
      },
     
      formatForChart(objectList) {
        const newList = objectList.map((object)=>{
          return [object.fuel, object.perc]})
        newList.unshift(["Fuel", "Percentage"])
        return newList
      },
      getFilterDate(){
        return `/${this.dateFrom}/${this.dateTo}`
      },
      filterByDate(){
        this.fetchData(this.getFilterDate())
      }
  },
  components: {
    'display-chart': DisplayChart
  }
      
}
</script>

<style>

</style>