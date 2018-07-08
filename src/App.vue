<template>
  <div id="app">
    <img src="./assets/logo.png">
    <h1>Vue Calculator Sample</h1>
    <calculator />
  </div>
</template>

<script>
import Calculator from './components/Calculator'

export default {
  name: 'app',
  components: {
    Calculator
  }
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

h1{
  margin: 10px;
  color:darkseagreen;
  font-family:Arial, Helvetica, sans-serif;
}
</style>
