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
    categories: [] as any[]
  }
})


onMounted(async () => {
  try {
    const response = await axios.get(import.meta.env.VITE_API_URL)
    console.log(response.data)
    // let times = time(response.data.hourly.time)
    option.value.xaxis.categories = response.data.hourly.time
    serie.value[0].data = response.data.hourly.temperature_2m
    api.value = response.data



  } catch (error) {
    console.error("Erro ao buscar dados:", error)
  }
});


// function time(value:string[]):string[] {
//   let valor = []
//   for(let i =0; i <value.length; i++ ){
//     valor.push(value[i].split('T')[1])
//   }

//   return valor
// }
</script>

<template>
  <!-- <v-container> -->

  <v-container class="teste3">
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

</template>

<style>
template {
  background: linear-gradient(45deg, #121212, #1e1e1e); /* Gradiente de fundo preto */
  color: white; /* Garantir que o texto fique branco */
  font-family: Arial, sans-serif;
}

/* Estilo dos cards */
.custom-card1 {
  max-width: 300px;
  margin: auto;
  padding: 16px;
  text-align: center;
  background-color: #2c2c2c; /* Cor de fundo dos cards, mais suave que o preto puro */
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.2); /* Sombra para dar destaque */
  border: 2px solid #444; /* Borda mais suave */
  border-radius: 1rem;
}

/* Estilo para o texto dos cards */
.sunrise-time, .sunset-time, .temperature-max, .temperature-min {
  font-size: 2rem; /* Aumenta o tamanho do texto */
  font-weight: bold;
}

.sunrise-time {
  color: #ff9800; /* Cor para o nascer do sol */
}

.sunset-time {
  color: #f44336; /* Cor para o pôr do sol */
}

.temperature-max {
  color: #f3aa21; /* Cor para a temperatura máxima */
}

.temperature-min {
  color: #2196f3; /* Cor para a temperatura mínima */
}

/* Estilo de loading */
.v-skeleton-loader {
  background-color: #444; /* Cor de fundo para o carregamento */
}


.custom-card {
  width: 100%;
  height: 100% ;
  border-radius: 1rem;
  padding: 0;
  /* background-color: blueviolet; */
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
  /* background-color: pink; */
}

.teste3 {
  width: 100%;
  height: 100vh;
  align-items: center;
  /* background-color: aqua; */
  

}

.teste4 {
  height: 70%;
  /* background-color: blue; */
}
.row1{
  margin-top: 13% !important;
  /* background-color: #4caf50; */
}

</style>
