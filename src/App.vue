<template>
  <div id="app">
    <double-dice :max-roll-time='6'></double-dice>
  </div>
</template>

<script>
import DoubleDice from "@/views/DoubleDice";

export default {
  name: 'App',
  components: {
    DoubleDice
  }
}
</script>

<style>
body{
  margin: 0;
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin: 0;
}
</style>
