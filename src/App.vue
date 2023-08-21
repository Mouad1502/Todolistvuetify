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
          <v-list-item-subtitle class="title pb-6">
            Stay productive!
          </v-list-item-subtitle>
          
          <v-list-item prepend-icon="mdi-format-list-checks" title="List" value="list" to="/"></v-list-item>
          <v-list-item prepend-icon="mdi-forum" title="About" value="about" to="/about"></v-list-item>
        </v-list>
      </v-navigation-drawer>

      <v-app-bar
        color="teal-darken-4"
      >
        <template v-slot:image>
          <v-img
            gradient="to top right, rgba(19,84,122,.8), rgba(128,208,199,.8)"
          ></v-img>
        </template>

        <template v-slot:prepend>
          <v-app-bar-nav-icon @click="drawer=!drawer"></v-app-bar-nav-icon>
        </template>

        <v-app-bar-title>To-Do List</v-app-bar-title>

        <v-spacer></v-spacer>

        <v-btn icon>
          <v-icon>mdi-magnify</v-icon>
        </v-btn>

        <v-btn icon>
          <v-icon>mdi-dots-vertical</v-icon>
        </v-btn>
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