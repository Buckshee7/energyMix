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
          .then(data => this.generationMix = this.formatForChart(data.data))
      },
     
      formatForChart(data) {
        const objectList = Array.isArray(data) ? this.averager(data):data.generationmix
        console.log(objectList)
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
      },

      averager(list){
        let newListOfObjects = []
        for(let i = 0; i<list.length; i++){
            for(let j = 0; j<list[i].generationmix.length; j++){
                if (!newListOfObjects[j]) {
                    newListOfObjects[j] = {'fuel':list[i].generationmix[j].fuel, 'perc':list[i].generationmix[j].perc}
                } else {
                    newListOfObjects[j].perc += list[i].generationmix[j].perc
                }
            }
        }
        newListOfObjects.forEach((object)=>{
            object.perc = object.perc/list.length
        })
        return newListOfObjects
      }

  },
  components: {
    'display-chart': DisplayChart
  }
      
}
</script>

<style>

</style>