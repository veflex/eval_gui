<template>
  <div id="app">
    <div id="nav">
      <!-- <router-link to="/">Eval</router-link> | -->
      <h1>Logo super beau de mon site</h1>
    </div>
    <router-view/>
  </div>
</template>

<style lang="scss">
#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
#nav {
  a {
    font-weight: bold;
    color: #2c3e50;
    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
h1 {
  margin: 0;
  padding: 10px;
}
</style>
