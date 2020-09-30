<template>
  <v-app id="app">
    <v-main class="secondary--text">
        <router-view></router-view>
    </v-main>
  </v-app>
</template>

<script>
export default {
  name: "App",
  data: () => ({
    //
  })
};
</script>

<style>
#app {
  background-color: black;
}
</style>
