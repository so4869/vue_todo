<template>
  <div id="app">
    <div class="logo">
      <img src="./assets/logo.png">
    </div>

    <h1>gondr todo application</h1>
    <div>
      <router-view></router-view>
    </div>
  </div>
</template>

<script>
export default {
  name: 'app',
  data () {
    return {
      msg: 'Welcome to Your Vue.js App'
    }
  }
}
</script>

<style>

*{
  margin: 0;
  padding: 0;
}

#app {
  width: 1200px;
  margin: 0 auto;
  display: flex;
  justify-content: center;
  flex-direction: column;
}

.logo {
  display: flex;
  justify-content: center;
}

.logo-text {
  text-align: center;
}

.router {
  width: 100%;
  margin: 10px;
}
</style>
