<template>
  <div id="app">
    <CalendarMonth />
  </div>
</template>

<script>
import CalendarMonth from './components/CalendarMonth.vue'

export default {
  name: 'App',
  components: {
    CalendarMonth
  }
}
</script>

<style>
#app {
  
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 30px;
}
body {
  font-family: Century Gothic;
  font-weight: 100;
}
.month-header {
  display: flex;
  justify-content: space-between;
  background-color: #fff;
  padding: 10px;
}
</style>
