<script setup lang="ts">
import { ref, onMounted } from 'vue'
import axios from "axios"
// -21.7434194,-43.3583964


const loading = ref(true)

// const api = ref<ApiResponse>()
const api = ref()
const serie = ref([
  {
    name: 'temperatura',
    data: [] as any[]
  }
])
const option = ref({
  xaxis: {
    name: "hora",
    categories: [] as any[]
  },
  tooltip: {
    theme: 'dark',
  },
  chart: {
    id: 'chart',
    toolbar: {
      show: false
    },
  }
})


onMounted(async () => {
  try {
    const response = await axios.get(import.meta.env.VITE_API_URL)
    console.log(response.data)
    let times = time(response.data.hourly.time)
    option.value.xaxis.categories = times
    serie.value[0].data = response.data.hourly.temperature_2m
    api.value = response.data



  } catch (error) {
    console.error("Erro ao buscar dados:", error)
  }
});


function time(value: string[]): string[] {
  let valor = []
  for (let i = 0; i < value.length; i++) {
    valor.push(value[i].split('T')[1])
  }

  return valor
}
</script>

<template>
  <!-- <v-container> -->

  <v-container>
    <v-row class="row1" no-gutters>
      <v-col>
        <v-sheet class="pa-2 ma-2 bg-transparent">
          <v-card class="custom-card1">
            <v-card-title class="text-h5 text-center">Nascer do Sol</v-card-title>
            <v-card-text class="d-flex justify-center align-center">
              <div v-if="api" class="sunrise-time">
                {{ api.daily.sunrise[0].split('T')[1] }}
              </div>
              <v-skeleton-loader v-else :loading="loading" height="50" width="100" type="text" />
            </v-card-text>
          </v-card>

        </v-sheet>
      </v-col>

      <v-col>
        <v-sheet class="pa-2 ma-2 bg-transparent">
          <v-card class="custom-card1">
            <v-card-title class="text-h5 text-center">Pôr do Sol</v-card-title>
            <v-card-text class="d-flex justify-center align-center">
              <div v-if="api" class="sunset-time">
                {{ api.daily.sunset[0].split('T')[1] }}
              </div>
              <v-skeleton-loader v-else :loading="loading" height="50" width="100" type="text" />
            </v-card-text>
          </v-card>

        </v-sheet>
      </v-col>

      <v-col>
        <v-sheet class="pa-2 ma-2 bg-transparent">
          <v-card class="custom-card1">
            <v-card-title class="text-h5 text-center">Temperatura Máxima</v-card-title>
            <v-card-text class="d-flex justify-center align-center">
              <div v-if="api" class="temperature-max">
                {{ api.daily.temperature_2m_max[0] }}°C
              </div>
              <v-skeleton-loader v-else :loading="loading" height="50" width="100" type="text" />
            </v-card-text>
          </v-card>

        </v-sheet>
      </v-col>

      <v-col>
        <v-sheet class="pa-2 ma-2 bg-transparent">
          <v-card class="custom-card1">
            <v-card-title class="text-h5 text-center">Temperatura Mínima</v-card-title>
            <v-card-text class="d-flex justify-center align-center">
              <div v-if="api" class="temperature-min">
                {{ api.daily.temperature_2m_min[0] }}°C
              </div>
              <v-skeleton-loader v-else :loading="loading" height="50" width="100" type="text" />
            </v-card-text>
          </v-card>
        </v-sheet>
      </v-col>
    </v-row>

    <v-row no-gutters>
      <v-col>
        <v-sheet class="pa-2 ma-2 bg-transparent">
          <v-card title="Temperatura" class="custom-card">
            <div class="test">
              <div v-if="api" class="apexchart">
                <apexCharts type="line" :series="serie" :options="option" class="chart" height="100%" mode="light" />
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

</template>

<style scoped>
.custom-card1 {
  text-align: center;
  background-color: #2c2c2c;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2);
  border: 2px solid #444;
  border-radius: 1rem;
}

.sunrise-time,
.sunset-time,
.temperature-max,
.temperature-min {
  font-size: 2rem;
  font-weight: bold;
}

.sunrise-time {
  color: #ff9800;
}

.sunset-time {
  color: #f44336;
}

.temperature-max {
  color: #f3aa21;
}

.temperature-min {
  color: #2196f3;
}

.v-skeleton-loader {
  background-color: #444;
}

.custom-card {
  border-radius: 1rem;
  padding: 0;
  align-items: center;

}

.chart {
  height: 100%;
  width: 100%;
}

@media (min-width: 601px) and (max-width: 700px) {
  .apexchart {
    width: 100%;
    height: 35vh;

  }
}

@media (max-width: 600px) {
  .apexchart {
    width: 100%;
    height: 40vh;

  }
}



.row1 {
  padding-top: 13% !important;

}

.apexchart {
  width: 100%;
  height: 30vh;

}
</style>
