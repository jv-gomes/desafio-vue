<script setup lang="ts">
import { ref } from 'vue'

import { useDisplay } from 'vuetify'
const { mobile } = useDisplay()


const drawer = ref(true)
const rail = ref(false)
</script>
<template>
  <div v-if="!mobile"> 
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
      <RouterLink to="/"><v-list-item prepend-icon="mdi-home-city" title="Home" value="home" >
        </v-list-item></RouterLink>
      <RouterLink to="/dashboard"><v-list-item prepend-icon="mdi-chart-line" title="Dashboard" value="dashboard" />
      </RouterLink>
      <!-- <RouterLink to="/login"><v-list-item prepend-icon="mdi-account-group-outline" title="Login" value="login" />
      </RouterLink> -->
    </v-list>
  </v-navigation-drawer>

</div>
<div v-else>
  <v-app-bar>
    <!-- Home Item -->
    <RouterLink to="/">
      <v-list-item 
        prepend-icon="mdi-home-city" 
        title="Home" 
        value="home" 
        class="mr-5 list-item-hover"
      />
    </RouterLink>

    <!-- Dashboard Item -->
    <RouterLink to="/dashboard">
      <v-list-item 
        prepend-icon="mdi-chart-line" 
        title="Dashboard" 
        value="dashboard"  
        class="list-item-hover"
      />
    </RouterLink>
  </v-app-bar>
</div>

</template>

<style scoped>
a {
  display: block;
  color: white;
  text-decoration: none;
}



</style>