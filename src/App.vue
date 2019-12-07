<template>
  <v-app id="inspire">
    <app-bar/>
    <main-content/>
  </v-app>
</template>

<script>
  import AppBar from './components/AppBar.vue'
  import MainContent from './components/MainContent.vue'
  export default {
    components: {
      AppBar,
      MainContent
    }
  }
</script>
