<template>
 <!-- <img alt="Vue logo" src="./assets/logo.png"> -->
 <!-- <HelloWorld msg="Welcome to Your Clase 2/9" msg2="Es una prueba de herencia"/>-->
  <TaskComponent/>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import TaskComponent from './components/TaskComponent.vue'

export default {
  name: 'App',
  components: {
   // HelloWorld,
    TaskComponent
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
