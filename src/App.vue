<template>
  <v-app id="App">
    <v-app-bar app color="green" dark>
      <div id="app-bar-left-side" class="d-flex">
        <v-app-bar-nav-icon id="menu" />
        <v-toolbar-title class="d-flex align-center">
          Gravador de Atividades
        </v-toolbar-title>
      </div>
      <div id="app-bar-right-side">
        <a-b-date-picker />
      </div>
    </v-app-bar>
    <home />
    <!-- <v-main>
      <HelloWorld />
    </v-main> -->
  </v-app>
</template>

<script>
import Home from './components/Home.vue'
import ABDatePicker from './modules/app-bar/ABDatePicker.vue';

export default {
  name: 'App',

  components: {
    Home,
    ABDatePicker
  },

  data: () => ({
  }),

  computed: {
  },

  methods: {
  }
};
</script>

<style>
* {
  height: 100%;
  width: 100%;
}

#App {
  background: black !important;
  color: white !important;
}

#app-bar-right-side {
  width: 260px;
}
</style>
