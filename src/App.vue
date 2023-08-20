<template>
  <v-app id="inspire">
    <v-navigation-drawer
      v-model="drawer"
      floating permanent
      >
        <v-list
          density="compact"
          nav
        >
          <v-list-item-title>
            Application
          </v-list-item-title>
          <v-list-item-subtitle class="title">
            Stay productive!
          </v-list-item-subtitle>
          <v-list-item prepend-icon="mdi-view-dashboard" title="Home" value="home" to="/"></v-list-item>
          <v-list-item prepend-icon="mdi-forum" title="About" value="about" to="/about"></v-list-item>
        </v-list>
      </v-navigation-drawer>

    <v-app-bar>
      <v-app-bar-nav-icon @click="drawer=!drawer" ></v-app-bar-nav-icon>

      <v-app-bar-title>Application</v-app-bar-title>
    </v-app-bar>

    <v-main>
      <router-view/>
    </v-main>
  </v-app>
</template>

<script setup>
  import { ref } from 'vue'

  const drawer = ref(null)
</script>

<script>
  export default {
    data: () => ({ drawer: null}),
  }
</script>