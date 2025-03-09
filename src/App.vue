<script setup lang="ts">
  import {  RouterView } from 'vue-router'
  import Menu from '@/components/Menu.vue'

</script>

<template>
  <v-app >
    <v-main >
      <v-container fluid >
    <v-row no-gutters  >
        <Menu />
      <v-col >
        <RouterView />
      </v-col>
    </v-row>
  </v-container>
    </v-main>
  </v-app>
</template>


<style>
.apexcharts-text{

  fill:rgb(134, 130, 130)
} 
</style>