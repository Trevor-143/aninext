<template>
  <nav class="navBar">
    <router-link to="/">
      <img src="./assets/anime.png" alt="aninext">
    </router-link>
    <form>
      <input type="text" placeholder="which anime...">
      <button>Search</button>
    </form>
  </nav>
  <router-view/>
</template>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@100;200;300;400;500;600;700;800;900&display=swap');

body {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'poppins', sans-serif;
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #000000;
}
#app {
  max-width: 1200px;
  width: 100%;
}
.navBar {
  padding-top: 1rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.navBar a {
  text-decoration: none;
}
.navBar img {
  width: 50px;
  height: auto;
}
.navBar form input {
  padding: 0.5rem;
  border: none;
  background-color: #1d1d1d;
  color: #fff;
  border-top-left-radius: 0.5rem;
  border-bottom-left-radius: 0.5rem;
}
.navBar form input::placeholder {
  color: #afafaf;
}
.navBar form input:focus {
  outline: none;
}
.navBar form button {
  border: none;
  padding: 0.5rem;
  color: #000;
  background-color: #fff;
  border-top-right-radius: 0.5rem;
  border-bottom-right-radius: 0.5rem;
}

/* #app {
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
} */
</style>
