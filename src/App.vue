<template>
  <div id="app">
    <backgrand></backgrand>
    <router-view/>
  </div>
</template>

<script>
import Backgrand from '@/components/Backgrand'
export default {
  name: 'App',
  components: {Backgrand}
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
