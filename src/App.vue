<template>
  <v-app class="main">
    <!-- <v-app-bar
      app
      color="cyan darken-1"
      dark
    >
    </v-app-bar> -->

    <v-main>
      <router-view/>
    </v-main>
    <footer class="text-center">
      Tribunal Supremo de Justicia
    </footer>
  </v-app>
</template>

<script>

export default {
  name: 'App',

  data: () => ({
    //
  }),
};
</script>
<style >
 .main{
  background: #9e9e9e !important; 
 }
</style>
