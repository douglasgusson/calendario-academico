<template>
  <div id="app">
    <Calendario title="Calendário SI (2020)"/>
  </div>
</template>

<script>
import Calendario from './components/Calendario.vue'

export default {
  name: 'App',
  components: {
    Calendario
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
