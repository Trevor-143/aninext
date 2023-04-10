<template>
  <nav class="navBar">
    <router-link to="/">
      <img src="./assets/anime.png" alt="aninext" >
    </router-link>
    <form @submit.prevent="getAnime()">
      <input type="text" placeholder="which anime..." v-model="searchText" >
      <button>Search</button>
    </form>
  </nav>
  <router-view/>
  <MainFooter />
</template>

<script>
  import MainFooter from "@/components/MainFooter";
  import { ref } from "vue";
  import { useRoute } from 'vue-router'

  export default {
    components: {
      MainFooter
    },
    setup() {
      const foundAnime = ref([])
      const resultsHeading = ref('')
      const searchText = ref('')
      const router = useRoute()
  
      const getAnime = () => {
        if (searchText.value != '') {
          this.$router.push({path: '/SearchAnime/', query:{key: searchText.value}})
          // document.querySelector('.hResults').innerHTML = `Did you search for ${searchText.value} ?`
          // fetch(`https://api.jikan.moe/v4/anime?q=${searchText.value}`)
          // .then(res => res.json())
          // .then(data => {
          //   console.log(data)
          //   foundAnime.value = data.data
          // })
        }
        // if (searchText.value == '') {
        //   document.querySelector('.hResults').innerHTML = ''
        //   foundAnime.value = null
        // }
      }
      const removeSearched = () => {
        document.querySelector('.hResults').innerHTML = ''
        foundAnime.value = null
      }
      const handleSearch = () => {
        
      }
      return {
        searchText,
        foundAnime,
        getAnime,
        removeSearched
        
      }
    }
  }
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Poppins:wght@100;200;300;400;500;600;700;800;900&display=swap');
* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
  font-family: 'poppins', sans-serif;
  /* outline: 1px red solid; */
}

body {
  display: flex;
  align-items: center;
  justify-content: center;
  background-color: #000000;
}
#app {
  max-width: 1200px;
  width: 100%;
  margin: 0 1rem;
  padding: 1rem;
}
.navBar {
  padding-top: 1rem;
  display: flex;
  align-items: center;
  justify-content: space-between;
  /* margin: 0 1rem; */
}
@media(max-width:600px) {
  .navBar {
    flex-direction: column;
  }
}
.navBar a {
  text-decoration: none;
}
.navBar img {
  width: 50px;
  height: auto;
}
.navBar form {
  display: flex;
  width: 100%;
  align-items: center;
  justify-content: flex-end;
}
.navBar form input {
  padding: 0.7rem;
  border: none;
  background-color: #1d1d1d;
  color: #fff;
  border-top-left-radius: 0.5rem;
  border-bottom-left-radius: 0.5rem;
  max-width: 600px;
  width: 100%;
}
.navBar form input::placeholder {
  color: #afafaf;
}
.navBar form input:focus {
  outline: none;
}
.navBar form button {
  border: none;
  padding: 0.7rem;
  color: #000;
  background-color: #fff;
  border-top-right-radius: 0.5rem;
  border-bottom-right-radius: 0.5rem;
}

.results {
  margin-top: 3rem;
  margin-bottom: 2rem;
}
.hResults {
  font-size: 15px;
  color: #fff;
  margin-bottom: 1rem;
}

.rList {
  display: grid;
  gap: 1rem;
  grid-template-columns: repeat(auto-fit, minmax(8rem, 1fr));
}
.rList a {
  text-decoration: none;
  color: #fff;
  position: relative;
  height: 200px;
  border: solid 2px #1d1d1d;
  border-radius: 1rem;
  overflow: hidden;
}
.rList a img {
  width: 100%;
  height: 100%;
  object-fit: cover;
}
.foundInfo {
  padding: 0.5rem;
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  background-image: linear-gradient(to top, rgba(0, 0, 0, 1), rgba(0, 0, 0, 0.5));
  border-top-left-radius: 1rem;
  border-top-right-radius: 1rem;
}
.foundInfo h3 {
  display: -webkit-box;
  -webkit-line-clamp: 2;
  -line-clamp: 2;
  -webkit-box-orient: vertical;
  overflow: hidden;
  font-size: 14px;
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
