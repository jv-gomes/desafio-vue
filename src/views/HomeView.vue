<script setup lang="ts">

</script>

<template>
  <v-container class="fill-height">
    <v-responsive class="align-centerfill-height mx-auto  responsive">
      <v-img class="mb-4" height="150" src="../../public/favicon.ico" />

      <div class="text-center">
        <div class="text-body-2 font-weight-light mb-n1"> Bem vindo ao</div>

        <h1 class="text-h2 font-weight-bold">TempToday</h1>
      </div>

      <div class="py-4" />

      <v-row>
        <v-col cols="12">
          <v-card class="py-4" color="darkgrey" prepend-icon="mdi-thermometer" rounded="lg" variant="elevated">

            <template #subtitle>
              <div class="text-cards">
                A temperatura do seu dia, a qualquer momento, em qualquer lugar.
              </div>
            </template>

          </v-card>
        </v-col>
        <v-col cols="12">
          <v-card class="py-4" color="darkgrey" prepend-icon="mdi-weather-sunny" rounded="lg" variant="elevated">

            <template #subtitle>
              <div class="text-cards">
                Saiba exatamente o clima onde você está, para um dia mais preparado!
              </div>
            </template>

          </v-card>
        </v-col>
        <v-col cols="12">
          <v-card class="py-4 " color="darkgrey" prepend-icon="mdi-map-marker-radius" rounded="lg" variant="elevated">

            <template #subtitle>
              <div class="text-cards">
                O clima do seu destino, na ponta dos dedos. Conecte-se com o tempo.
              </div>
            </template>

          </v-card>
        </v-col>

      </v-row>
    </v-responsive>
  </v-container>
</template>

<style scoped>
.responsive {
  max-width: 900px;
}

.text-cards {
  font-size: 1.25rem;
  font-weight: bold;
  margin: 0.67em 0;
  white-space: normal;
}

@media (min-width: 601px) and (max-width: 700px) {
  .responsive {
    max-width: 600px;
  }

  .text-cards {
    font-size: 1rem;
    font-weight: bold;
    margin: 0.67em 0;
    white-space: normal;
  }
}

@media (max-width: 600px) {
  .responsive {
    max-width: 400px;
  }

  .text-cards {
    font-size: 0.85rem;
    font-weight: bold;
    margin: 0.67em 0;
    white-space: normal;

  }

  @media (max-width: 400px) {
    .responsive {
      max-width: 350px;
    }

    .text-cards {
      font-size: 0.85rem;
      font-weight: bold;
      margin: 0.67em 0;
      white-space: normal;

    }
  }
}
</style>