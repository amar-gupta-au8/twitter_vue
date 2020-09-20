<template>
  <div id="app">
    <nav>
      <div class="navigation_logo">
        <router-link to="/">
          Twitter
        </router-link>
      </div>
      <div class="navigation_user">{{ user.userName }}</div>
    </nav>
    <router-view />
  </div>
</template>

<script>
export default {
  name: 'App',
  data() {
    return {
      user: {
        userName: '@theamargupta',
      },
    };
  },
};
</script>

<style lang="scss">
body {
  margin: 0;
  a {
    text-decoration: none;
    color: inherit;
  }
}
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  min-height: 96vh;
  background-color: #f3f5fa;
}
nav {
  display: flex;
  align-items: center;
  justify-content: space-between;
  padding: 10px 5%;
  background-color: #00acee;
  color: white;
  .navigation_logo,
  .navigation_user {
    font-weight: bold;
    font-size: 24px;
  }
}
</style>
