<template>
  <nav>
    <div class="links">
    <router-link to="/">Criar Produto</router-link>
    <router-link to="/about">Listagem</router-link>
    <router-link to="/dispatch">Retirada</router-link>
  </div>
  </nav>
  <router-view/>
</template>

<style>
  body{
    background: rgb(192, 192, 192);
  }
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
  margin: 0px 12px ;
}

nav a.router-link-exact-active {
  color: #fff;
}
</style>