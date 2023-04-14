<template>
  
  <div class="home">

    <div class="random">
      <img class="backImg" :src="randomImgURL" :alt="random.title">
      <router-link :to="'/about/'+random.mal_id" class="randomAnime">
        <img :src="random.images.jpg.image_url" :alt="random.title">
        <div class="randomSide" id="firstSide">
          <h3>{{ random.title }}</h3>
          <p>{{ random.synopsis }}</p>
          <div class="randomTags">
            <h4>{{ random.episodes }} episodes</h4>
            <h4>{{ random.score }}/10 score</h4>
            <h4>{{ random.rating }}</h4>
            <h4>From {{ random.source }}</h4>
          </div>
        </div>
      </router-link>
      
    </div>

    <div class="randomSide" id="side">
      <h3>{{ random.title }}</h3>
      <p>{{ random.synopsis }}</p>
      <div class="randomTags">
        <h4>{{ random.episodes }} episodes</h4>
        <h4>{{ random.score }}/10 score</h4>
        <h4>{{ random.rating }}</h4>
        <h4>From {{ random.source }}</h4>
      </div>
    </div>

    <div class="Anime">
      <h2 class="animeHead"></h2>
      <div class="AnimeList">
        <router-link :to = "'/about/'+ anime.mal_id" class="animeListItem" v-for="anime in topAnime" :key="anime.mal_id">
          <img :src="anime.images.webp.image_url" :alt="anime.title">
          <div class="animeListItemInfo">
            <h3>{{ anime.title_english }}</h3>
            <p class="desc">{{anime.synopsis}}</p>
            <h4>From {{ anime.source }}</h4>
            <h4>{{ anime.score }}/10</h4>
          </div>
        </router-link>
      </div>
    </div>

    <div class="Anime">
      <h2 class="wait"></h2>
      <div class="AnimeList">
        <router-link :to = "'/about/'+ anime.mal_id" class="animeListItem" v-for="anime in upcoming" :key="anime.mal_id">
          <img :src="anime.images.webp.image_url" :alt="anime.title">
          <div class="animeListItemInfo">
            <h3>{{ anime.title_english }}</h3>
            <p class="desc">{{anime.synopsis}}</p>
            <h4>From {{ anime.source }}</h4>
            <h4>{{ anime.aired.string }}</h4>
          </div>
        </router-link>
      </div>
    </div>

    <div class="charas">
      <h3 class="h1"></h3>
      <section>
        <router-link :to="'/character/' + chara.mal_id " v-for="chara in topCharacters" :key="chara.mal_id">
          <img :src="chara.images.webp.image_url" :alt="chara.name">
          <h3>{{ chara.name }}</h3>
        </router-link>
      </section>
    </div>

  </div>
</template>

<script>
// @ is an alias to /src
import { ref, onBeforeMount, onMounted } from "vue";

export default {
  name: 'HomeView',
  components: {
    
  },
  setup() {
    const topAnime = ref([])
    const randomImgURL = ref('') 
    const randomAnime = ref([])
    const random = ref([])
    const upcoming = ref([])
    const topCharacters = ref([])
    

    onBeforeMount(() => {
      setTimeout(() => {
        fetch(`https://api.jikan.moe/v4/top/anime`)
        .then(resp => resp.json())
        .then(data => {
          randomAnime.value = Math.floor(Math.random() * (data.data.length))
          random.value = data.data[randomAnime.value]
          randomImgURL.value = data.data[randomAnime.value].trailer.images.maximum_image_url
          // console.log(random.value)
        })
      }, 10);

      setTimeout(() => {
        fetch(`https://api.jikan.moe/v4/top/anime`)
        .then(res => res.json())
        .then(data => {
          // console.log(data)
          topAnime.value = data.data
          if(topAnime.value != null) {
            document.querySelector('.animeHead').innerHTML = "Anime to watch"
          }
        })
      }, 1000)

      setTimeout(() => {
        fetch(`https://api.jikan.moe/v4/seasons/upcoming`)
        .then(res => res.json())
        .then(data => {
          // console.log(data)
          upcoming.value = data.data
          if(upcoming.value != null) {
            document.querySelector('.wait').innerHTML = "looking forwarch to.."
          }
        })
      }, 2000)
      
    })
    onMounted(() => {
      setTimeout(() => {
        fetch(`https://api.jikan.moe/v4/top/characters`)
        .then(res => res.json())
        .then(data => {
          topCharacters.value = data.data
          // console.log(topCharacters.value)
          if(topCharacters.value != null) {
            document.querySelector('.h1').innerHTML = "top characters"
          }
        })
      }, 3000);
    })
    
    
    return {
      topAnime,
      random,
      upcoming,
      topCharacters,
      randomImgURL
    }
  }
}
</script>

<style>
  .random {
    width: 100%;
    position: relative;
    margin-top: 1rem;
    border-radius: 1rem;
    /* overflow: hidden; */
    max-height: 300px;
    min-height: 300px;
    height: 100%;
    
  }
  .backImg {
    width: 100%;
    height: 100%;
    max-height: 300px;
    object-fit: cover;
    border-radius: 1rem;
    height: 100%;
  }
  .random a {

    text-decoration: none;
    color: #fff;
    display: flex;
    align-items: center;
    flex-direction: row;
    position: absolute;
    top: 0;
    bottom: 0;
    left: 0;
    right: 0;
    padding: 1rem;
    background-image: linear-gradient(to right, rgba(0, 0, 0, 1), rgba(0, 0, 0, .4));
  }
  .random a img {
    border-radius: 1rem;
    height: 90%;
    min-width: 100px;
    min-height: 140px;
  }
  #side {
    display: none;
  }

  @media (max-width: 700px) {
    #app {
      margin: 0 1rem;
    }
    #firstSide {
      display: none;
    }
    .random {
      width: 100%;
      /* margin: 1rem; */
    }
    #side {
      display: flex;
      width: 100%;
      /* padding: 1rem; */
    }
    #side .randomSide {
      margin: 0;
    }
    #side p {
      /* padding: 0.5rem 0; */
      display: -webkit-box;
      overflow: hidden;
      -webkit-line-clamp: 2;
            -line-clamp: 2;
      -webkit-box-orient: vertical;
      font-size: 13px;
      margin: 0;
    }

    #side h3, #side p {
      color: #fff;
    }
    #side .randomTags {
      padding-top: 0.5rem;
    }
    .random a img {
      max-width: 200px;
    }
  }
  .randomSide {
    display: flex;
    flex-direction: column;
    /* min-width: 250px; */
    max-width: 800px;
    width: 100%;
  }
  .randomSide p {
    display: -webkit-box;
    overflow: hidden;
    -webkit-line-clamp: 3;
          -line-clamp: 3;
    -webkit-box-orient: vertical;
    font-size: 13px;
    margin: 1rem 0;

  }
  #firstSide {
    padding: 1.5rem;
  }
  .randomTags {
    display: flex;
    flex-direction: row;
    flex-wrap: nowrap;
    overflow-X: auto;
  }
  .ramdomTags::-webkit-scrollbar {
    display: none;
  }
  .randomTags h4 {
    width: fit-content;
    padding: 0.3rem 0.5rem;
    display: flex;
    white-space: nowrap;
    flex-direction: row;
    align-items: center;
    justify-content: center;
    background-color: #fff;
    color: #000;
    border-radius: 0.5rem;
    margin-right: 0.7rem;
  }
  .randomTags h4:nth-child(4) {
    background-color: #000;
    color: #fff;
    border: solid 2px #fff;
  }

  .Anime {
    margin-bottom: 1rem;
    /* padding: 0.5rem 1rem; */
  }
  .Anime h2 {
    color: #fff;
    font-size: 17px;
    margin-left: 1rem;
    margin-top: 2rem;
  }
  .AnimeList {
    display: grid;
    gap: 0.5rem;
    grid-template-columns: repeat(auto-fit, minmax(15rem, 1fr));
  }
  .AnimeList a {
    text-decoration: none;
  }
  @media(min-width:500px) {
    .AnimeList :nth-child(1), .AnimeList :nth-child(12), .AnimeList :nth-child(20) {
      grid-row: span 2;
      grid-column: span 2;
      height: 100%;
    }
    .AnimeList :nth-child(1) img, .AnimeList :nth-child(12) img, .AnimeList :nth-child(20) img {
      max-height: 90%;
    }
    .AnimeList :nth-child(1) .animeListItemInfo p, .AnimeList :nth-child(12) .animeListItemInfo p, .AnimeList :nth-child(20) .animeListItemInfo p {
      display: -webkit-box;
      overflow: hidden;
      -webkit-line-clamp: 3;
            -line-clamp:3;
      -webkit-box-orient: vertical;
      color: #dfdfdf;
      font-size: 14px;
    }
  }
  .animeListItem {
    width: 100%;
    height: 120px;
    overflow: hidden;
    border-radius: 1rem;
    display: flex;
    align-items: center;
    justify-content: flex-start;
    background-color: #1d1d1d;
    border: 2px solid rgba(29, 29, 29, 0);
    transition: 0.4s;
  }
  .animeListItem:hover {
    transform: translateY(-10px);
    background-color: #000000;
    border: 2px solid rgba(29, 29, 29, 1);
  }
  .animeListItem img {
    max-height: 80%;
    max-width: 30%;
    width: 100%;
    object-fit: cover;
    border-radius: 1rem;
    margin: 0.5rem;
  }
  .animeListItemInfo {
    padding-right: 1rem;
  }
  .animeListItemInfo h3, .animeListItemInfo h4 {
    margin: 0;
  }
  .animeListItemInfo h3 {
    overflow: hidden;
    display: -webkit-box;
    -webkit-line-clamp: 2;
            -line-clamp: 2;
    -webkit-box-orient: vertical;
    font-size: 15px;
    color: #f3f3f3;
  }
  .animeListItemInfo p {
    display: none;
  }
  .animeListItemInfo :nth-child(3) {
    color: #b8b8b8;
    font-size: 12px;
    margin: 0.2rem 0;
  }
  .animeListItemInfo :nth-child(4) {
    width: fit-content;
    padding: 0.3rem 0.7rem;
    background-color: #ffffff;
    color: #000000;
    border-radius: 0.5rem;
    font-size: 12px;
  }
  .h1 {
    font-size: 17px;
    margin-top: 2rem;
    color: #fff;
    margin-left: 1rem;
  }
  .charas section {
    display: flex;
    flex-direction: row;
    overflow: auto;
  }
  .charas section::-webkit-scrollbar {
    display: none;
  }
  .charas a {
    margin: 0.5rem;
    width: 100px;
    color: #c7c7c7;
    text-align: center;
    font-size: 13px;
    text-decoration: none;
  }
  .charas a img {
    width: 110px;
    height: 110px;
    object-fit: cover;
    border-radius: 50%;
    /* border: #ffffff solid 2px; */
  }
</style>
