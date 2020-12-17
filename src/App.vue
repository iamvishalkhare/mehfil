<template>
  <div id="app">
    <HelloWorld/>
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  components: {
    HelloWorld
  },
  created(){
      document.title = "Mehfil Meat"
  },
}
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@200&family=Roboto+Condensed:wght@300;400;700&display=swap');
@import url('https://fonts.googleapis.com/css2?family=Raleway:wght@800;900&display=swap');
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
body {
  background-image:    url("./assets/bg2.jpg");
  background-repeat: no-repeat;
  background-position: center center;
  background-attachment: fixed;
  background-size: cover;
  /* background: linear-gradient( rgba(0, 0, 0, 0.5), rgba(0, 0, 0, 0.5) ); */
}
</style>
