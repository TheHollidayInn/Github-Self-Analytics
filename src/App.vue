<template>
  <div id="app">
    <h1>Github Analytics</h1>
    <router-view/>
  </div>
</template>

<script>
export default {
  name: 'App'
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

body {
  color: #767ead;
  font-family: Nunito,sans-serif;
  background-image: linear-gradient(-15deg,#d3dbf8 25%,transparent 0),linear-gradient(15deg,#885fff 10%,transparent 0),linear-gradient(75deg,#fafaff 52%,transparent 0);
  width: 100%;
  height: 100vh;
}
</style>
