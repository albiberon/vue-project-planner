<template>
  <Navbar/>
  <router-view/>
</template>

<script>
import Navbar from "./components/Navbar.vue"

export default {
  components: { Navbar }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #555;
  max-width: 600px;
  margin: 0 auto;
}

body {
  background: #f2f2f2
}
</style>