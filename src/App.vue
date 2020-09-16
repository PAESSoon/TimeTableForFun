
<template>
  <div id="app">
    <main-page class="body" />
  </div>
</template>

<script>
import mainPage from './components/Main/MainPage.vue'

export default {
  
  components: {
    mainPage,
  },

  methods: {
  }
}
</script>

<style lang="less">
@import url('https://fonts.googleapis.com/css2?family=Merriweather+Sans:ital,wght@0,300;0,800;1,300;1,400&display=swap');
#app {
  font-family: 'Merriweather Sans', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}

body {
  background-color: #fcf8f3;
}

h1, h2 {
  font-weight: normal;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: inline-block;
  margin: 0 10px;
}

a {
  color: #42b983;
}

::-webkit-scrollbar-track {
  opacity: 0.5;
  background: #dfdfdf;
  border-radius: 4px;
}

::-webkit-scrollbar-thumb {
  opacity: 0.5;
  background: #8a8a8a;
  border-radius: 4px;
}
</style>
