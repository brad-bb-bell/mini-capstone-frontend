<script>
export default {
  data: function () {
    return {
      isLoggedIn: false,
    };
  },
  created: function () {},
  methods: {},
  watch: {
    $route: function () {
      this.isLoggedIn = !!localStorage.jwt;
    },
  },
};
</script>

<template>
  <nav>
    <router-link to="/products">Store</router-link>
    |
    <router-link to="/products/new">Add Product</router-link>
    |
    <router-link to="/signup" v-if="!isLoggedIn">Signup</router-link>
    |
    <router-link to="/login" v-if="!isLoggedIn">Login</router-link>
    |
    <router-link to="/logout" v-if="isLoggedIn">Logout</router-link>
  </nav>
  <router-view />
</template>

<style>
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
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
