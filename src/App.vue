<template>
  <div id="app">
    <board></board>
  </div>
</template>

<script>
import board from "@/components/board";

export default {
  name: 'App',

  components: {
    board
  }
}
</script>

<style>
#app {
  display: flex;
  height: 100%;
  align-items: center;
  justify-content: center;
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  background: #4c5bed;
}
</style>
