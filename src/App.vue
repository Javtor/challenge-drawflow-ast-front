<template>
  <Drawflow/>
</template>

<script>
import Drawflow from './components/Drawflow.vue'

export default {
  name: 'App',
  components: {
    Drawflow
  }
}
</script>

<style>
html {
  padding: 0;
  margin: 0;
  overflow: hidden;
  background: transparent;
}
 body {
  max-width: calc(100vw - 40px);
  max-height:  calc(100vh - 40px);
  margin: 20px;
  padding: 0;
  background-color: #181818;
  color: #f7f7f7;
}

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  margin: 0px;
  border-radius: 8px; 
  border: 1px solid #494949;
  text-align: center;
  min-height: calc(100vh - 40px);
}
</style>
