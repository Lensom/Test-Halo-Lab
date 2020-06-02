<template>
  <div id="app">
    <Home />
  </div>
</template>

<style lang="scss">
@import "assets/scss/index.scss";
</style>

<script>
import Home from "@/components/pages/Home";

export default {
  name: "app",
  components: {
    Home
  }
};
</script>
