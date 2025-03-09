<script setup lang="ts">
import { ref } from 'vue'

const drawer = ref(true)
const rail = ref(false)
</script>
<template>

  <v-navigation-drawer v-model="drawer" :rail="rail" permanent @click="rail = false">

    <v-list-item
          prepend-avatar="../../public/favicon.ico"
          title="TempToday"
          nav
        >
          <template v-slot:append>
            <v-btn
              icon="mdi-chevron-left"
              variant="text"
              @click.stop="rail = !rail"
            ></v-btn>
          </template>
</v-list-item>

    <v-divider></v-divider>

    <v-list nav>
      <RouterLink to="/"><v-list-item prepend-icon="mdi-home-city" title="Home" value="home">
        </v-list-item></RouterLink>
      <RouterLink to="/dashboard"><v-list-item prepend-icon="mdi-chart-line" title="Dashboard" value="dashboard" />
      </RouterLink>
      <!-- <RouterLink to="/login"><v-list-item prepend-icon="mdi-account-group-outline" title="Login" value="login" />
      </RouterLink> -->
    </v-list>
  </v-navigation-drawer>



</template>

<style>
a {
  display: block;
  color: white;
  text-decoration: none;
}
</style>