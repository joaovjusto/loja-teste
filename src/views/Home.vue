<template>
  <div class="home">
    <!-- <img alt="Vue logo" src="../assets/logo.png" /> -->
    <HelloWorld msg="Welcome to Your Vue.js App" />
  </div>
</template>

<script>
// @ is an alias to /src
import Principal from "@/components/Principal.vue";

export default {
  name: "home",
  components: {
    Principal
  }
};
</script>
