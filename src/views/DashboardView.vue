<script setup lang="ts">
import {ref, onMounted} from 'vue'
import axios from "axios"
// -21.7434194,-43.3583964

interface ApiResponse {
  latitude: number;
  longitude: number;
}



// const api = ref<ApiResponse>()
  const api = ref()
  const serie = ref([
  {
    name:'temperatura',
    data:[]
  }
])
  const option = ref({
  xaxis:{
    categories:[]
  }
})


  const lineChartSeries = ref([
  {
    name:'hora',
    data:[]
  }
])

const lineChartOptions = ref()



onMounted(async () => {
  try {
    const response = await axios.get(import.meta.env.VITE_API_URL)
    console.log(response.data)
    api.value = response.data
    serie.value[0].data = response.data.hourly.temperature_2m
    option.value.xaxis.categories = response.data.hourly.time
  } catch (error) {
    console.error("Erro ao buscar dados:", error)
  }
});


</script>

<template>
  <main>
    <!-- <v-container> -->


    <v-card title="Temperatura" 
    style="width: 50%; height: 100%; border-radius: 1rem; padding: 0;" 
     class="custom-card">
     <div class="test">
      <div v-if="api">
      <apexCharts 
      type="line"
      :series="serie"
      :options="option"
      class="chart"
       />
       </div>
    </div>
    </v-card>

<!-- </v-container> -->
    <!-- <div class="flex flex-col gap-16 p-24 items-center bg-gray-700">
      <h2>text </h2>
    <div class="w-1/3 bg-white rounded-xl p-4 " >
    <h2 class="text-x1 font-semibold"> Grafico Linha</h2>
    <apexCharts 
      type="line"
      :series="lineChartSeries"
      :options="lineChartOptions"
       /> -->

    <!-- </div> -->

    <!-- <div class="w-1/3 bg-white rounded-xl p-4 " >
    <h2 class="text-x1 font-semibold"> Grafico Barra</h2>
    <apexCharts 
      type="bar"
      :series="barChartSeries"
      :options="barChartOptions"
       />

    </div>

    <div class="w-1/3 bg-white rounded-xl p-4 " >
    <h2 class="text-x1 font-semibold"> Grafico Pizza</h2>
    <apexCharts 
      type="pie"
      :series="pieChartSeries"
      :options="pieChartOptions"
       />

    </div>

    <div class="w-1/3 bg-white rounded-xl p-4 " >
    <h2 class="text-x1 font-semibold"> Grafico Area</h2>
    <apexCharts 
      type="area"
      :series="barChartSeries"
      :options="barChartOptions"
       />

    </div> -->
  <!-- </div> -->
  </main>
</template>

<style>


.test{
    width: 97%;
}


.chart {

    height: 6%; /* Faz o gráfico ocupar toda a altura do card */
}
</style>
