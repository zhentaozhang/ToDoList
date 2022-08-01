<template>
  <svg-blue></svg-blue>
  <Home></Home>

</template>

<script>
import Home from "./components/Home.vue";
import SvgBlue from "./components/SvgBlue.vue";

export default {
  components: {
    Home,
    SvgBlue
  }
}
</script>


<style scoped>
* {
  padding: 0;
}
</style>
