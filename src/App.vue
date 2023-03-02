<template>
  <div id="app">
    <mybaby></mybaby>
  </div>
</template>

<script>
//这里mybaby可以取一个你喜欢的名字。
import mybaby from "./components/loadBuild.vue"

export default {
  name: 'App',
  components: {
    mybaby
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
}
</style>
