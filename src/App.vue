<template>
  <div id="app">
    <!-- <img alt="Vue logo" src="../assets/logo.png" /> -->
    <Header />
    <router-view></router-view>
  </div>
</template>

<script>
// @ is an alias to /src
import Header from "@/components/Header.vue";

export default {
  name: "app",
  components: {
    Header
  }
};
</script>
