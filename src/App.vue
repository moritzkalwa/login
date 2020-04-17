<template>
  <div id="app">
    <login-window />
  </div>
</template>

<script>
import LoginWindow from './components/LoginWindow.vue'

export default {
  name: 'App',
  components: {
    LoginWindow
  }
}
</script>

<style>
  #app {
    margin: 0;
    padding: 0;
  }
</style>
