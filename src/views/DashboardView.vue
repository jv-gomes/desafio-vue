<script setup lang="ts">
import { ref, onMounted } from 'vue'
import axios from "axios"
// -21.7434194,-43.3583964

interface ApiResponse {
  latitude: number;
  longitude: number;
}

const loading = ref(true)

// const api = ref<ApiResponse>()
const api = ref()
const serie = ref([
  {
    name: 'temperatura',
    data: []
  }
])
const option = ref({
  xaxis: {
    categories: []
  }
})


const lineChartSeries = ref([
  {
    name: 'hora',
    data: []
  }
])

const lineChartOptions = ref()

const units = ref()
const sunshine = ref()


onMounted(async () => {
  try {
    const response = await axios.get(import.meta.env.VITE_API_URL)
    console.log(response.data)
    api.value = response.data
    serie.value[0].data = response.data.hourly.temperature_2m
    option.value.xaxis.categories = response.data.hourly.time
    console.log(units)

    let hours = Math.floor(response.data.daily.daylight_duration[0]  / 3600);
    let minutes = Math.floor((response.data.daily.daylight_duration[0]  % 3600) / 60);
    let seconds = Math.floor(response.data.daily.daylight_duration[0]  % 60);

    units.value = `${String(hours).padStart(2, '0')}:${String(minutes).padStart(2, '0')}:${String(seconds).padStart(2, '0')}`;


     hours = Math.floor(response.data.daily.sunshine_duration[0] / 3600);
     minutes = Math.floor((response.data.daily.sunshine_duration[0]  % 3600) / 60);
     seconds = Math.floor(response.data.daily.sunshine_duration[0]  % 60);

     sunshine.value = `${String(hours).padStart(2, '0')}1:${String(minutes).padStart(2, '0')}2:${String(seconds).padStart(2, '0')}`;


  } catch (error) {
    console.error("Erro ao buscar dados:", error)
  }
});


</script>

<template>
    <!-- <v-container> -->

    <v-container class="teste3">
      <v-row class="mb-6" no-gutters>
        <v-col>
          <v-sheet class="pa-2 ma-2 bg-transparent">
            <v-card title="Nascer do sol">
                <div v-if="api">
                  {{  api.daily.sunrise[0].split('T')[1]}}
                </div>
                <div v-else>
                  <v-skeleton-loader :loading="loading" height="200" type="image">
                  </v-skeleton-loader>
                </div>
            </v-card>
          </v-sheet>
        </v-col>

        <v-col>
          <v-sheet class="pa-2 ma-2 bg-transparent">
            <v-card title="pôr do sol">
                <div v-if="api">
                  {{  api.daily.sunset[0].split('T')[1]}}
                </div>
                <div v-else>
                  <v-skeleton-loader :loading="loading" height="200" type="image">
                  </v-skeleton-loader>
                </div>
            </v-card>
          </v-sheet>
        </v-col>

        <v-col>
          <v-sheet class="pa-2 ma-2 bg-transparent">
            <v-card title="Temperatura maxima">
                <div v-if="api">
                  {{  api.daily.temperature_2m_max[0] }}
                </div>
                <div v-else>
                  <v-skeleton-loader :loading="loading" height="200" type="image">
                  </v-skeleton-loader>
                </div>
            </v-card>
          </v-sheet>
        </v-col>

        <v-col>
          <v-sheet class="pa-2 ma-2 bg-transparent">
            <v-card title="Temperatura minima">
                <div v-if="api">
                  {{ api.daily.temperature_2m_min[0] }}
                </div>
                <div v-else>
                  <v-skeleton-loader :loading="loading" height="200" type="image">
                  </v-skeleton-loader>
                </div>
            </v-card>
          </v-sheet>
        </v-col>
      </v-row>

      <v-row no-gutters class="teste4">
        <v-col class="h-100">
          <v-sheet class="pa-2 ma-2 h-50 bg-transparent">
            <v-card title="Temperatura" class="custom-card">
              <div class="test">
                <div v-if="api" class="teste2">
                  <apexCharts type="line" :series="serie" :options="option" class="chart" width="100%" height="100%" />
                </div>
                <div v-else>
                  <v-skeleton-loader :loading="loading" height="200" type="card">
                  </v-skeleton-loader>
                </div>
              </div>
            </v-card>
          </v-sheet>
        </v-col>

      </v-row>
    </v-container>






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
</template>

<style>

.custom-card{
  width: 100%; 
  height: 100%; 
  border-radius: 1rem; 
  padding: 0;
  /* background-color: blueviolet;  */
  align-items: center;

}

.test {
  width: 100%;
  height: 100%;
  /* background-color: yellow; */
}

.teste2 {
  width: 100%;
  height: 98%;
  /* background-color: red; */
}
.teste3{

  height: 100vh;
  /* background-color: aqua; */

}

.teste4{
  height: 70%;
  /* background-color: blue; */
}
.chart {

  height: 6%;
  /* Faz o gráfico ocupar toda a altura do card */
}
</style>
