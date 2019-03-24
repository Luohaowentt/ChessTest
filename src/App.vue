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

</style>
