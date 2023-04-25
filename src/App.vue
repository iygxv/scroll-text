<template>
  <div id="app">
    <scroll-text :text="'我打算那得看你看了打撒拉倒吧那可能看打了你打开啦'"/>
  </div>
</template>

<script>
import scrollText from './components/scroll-text.vue'

export default {
  name: 'App',
  components: {
    scrollText
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
