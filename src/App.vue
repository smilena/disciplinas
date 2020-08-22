<template>
  <div id="app">
    <h1>La informática y otras disciplinas</h1>
    <h2>"Sistemas sociales técnicamente implementados"</h2>
    <Graph />
  </div>
</template>

<script>
import Graph from './components/Graph.vue'

export default {
  name: 'App',
  components: {
    Graph
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
