<template>
  <div>
    <nav class="fixed bg-green-500 min-w-full p-5">
      <h1 class="font-semibold text-2xl text-white">Time</h1>
    </nav>
    <stopwatch/>
  </div>
</template>

<script>
import stopwatch from './components/stopwatch.vue'

export default {
  name: 'App',
  components: {
    stopwatch
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
