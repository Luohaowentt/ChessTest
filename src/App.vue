<template>
  <div id="app">
    <Background></Background>
    <router-view/>
  </div>
</template>

<script>
import Background from '@/components/Backgrand'
export default {
  name: 'App',
  components: {Background}
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
