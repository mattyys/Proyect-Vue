<template>
  <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
  <!-- <HelloWorld msg="Welcome to Your Clase 2/9" msg2="Es una prueba de herencia"/>-->
  <!-- <TaskComponent /> -->
  <!-- <ClaseTres/> -->
  <ControlGastos/>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
//import TaskComponent from './components/TaskComponent.vue'
//import ClaseTres from './components/ClaseTres.vue'
import ControlGastos from './components/ControlGastos.vue';

export default {
  name: 'App',
  components: {
    // HelloWorld,
    //TaskComponent,
    //ClaseTres
    ControlGastos
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
