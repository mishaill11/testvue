<template>
  <div id="app">
    <clientForm />
  </div>
</template>

<script>
import clientForm from './components/ClientForm.vue'

export default {
  name: 'App',
  components: {
    clientForm
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
