<template>
  <div id="app">
    <!--    <div id="nav"><router-link to="/">Home</router-link></div>-->
    <router-view />
  </div>
</template>

<style lang="scss" scoped>
body {
  background-color: blue;
}
* {
  box-sizing: border-box;
}
#app {
  max-width: 400px;
  margin: 0 auto;
  line-height: 1.4;
  font-family: Montserrat, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
h1 {
  text-align: center;
}
</style>
