<template>
  <div id="app">
    
    <MainPage/>
    
  </div>
</template>

<script>
//import HelloWorld from './components/HelloWorld.vue'
import MainPage from './components/MainPage.vue'

export default {
  name: 'app',
  components: {
    MainPage
  }
}
</script>

<style>

@import url('https://fonts.googleapis.com/css?family=Lobster&display=swap&subset=cyrillic');
@import url('https://fonts.googleapis.com/css?family=El+Messiri:700&display=swap&subset=cyrillic');

#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

body
{
  height: 100vh;
  overflow: hidden;
  /*background: linear-gradient(#f5af19, #f12711)*/
  /*background: linear-gradient(#DA4453, #89216B);*/
  background: linear-gradient(#ff6a00, #ee0979)
}
</style>
