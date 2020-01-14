<template>
  <div id="app">
    <!--<HelloWorld msg="Welcome to Your Vue.js App"/>-->
    <Clinic/>
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import Clinic from './components/Clinic.vue'

export default {
  name: 'app',
  components: {
    //HelloWorld
    Clinic
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
</style>
