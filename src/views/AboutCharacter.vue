<template >
    <div class="charas">
        <div class="cIntro">
            <img :src="imageURL" :alt="characterInfo.name">
            <div class="cIntroName">
                <h3>{{ characterInfo.name }}</h3>
                <h4>{{ characterInfo.name_kanji }}</h4>
                <p>From {{ bestAnime }}</p>
            </div>
        </div>
        <div class="cAbout">
            <h3>About {{characterInfo.name}}</h3>
            <p>{{characterInfo.about}}</p>
        </div>
        <div class="cAnime">
            <h2>{{characterInfo.name}}'s anime list</h2>
            <div class="cAnimeList">
                <div v-for="item in anime" :key="item.mal_id">
                    <img :src="item.anime.images.webp.image_url" :alt="item.title">
                    <div class="mini">
                        <h3>{{item.anime.title}}</h3>
                        <h3>{{item.role}}</h3>
                    </div>
                </div>
            </div>
        </div>
        <div class="cManga">
            <h2>{{characterInfo.name}}'s manga list</h2>
            <div class="cMangaList">
                <div v-for="item in manga" :key="item.mal_id">
                    <img :src="item.manga.images.webp.image_url" :alt="item.title">
                    <div class="mini">
                        <h3>{{item.manga.title}}</h3>
                        <h3>{{item.role}}</h3>
                    </div>
                </div>
            </div>
        </div>
        <div class="cVoice">
            <h1>{{ characterInfo.name }}' voice actors.</h1>
            <div class="cVoices">
                <div class="man" v-for="item in voices" :key="item.mal_id">
                    <img :src="item.person.images.jpg.image_url" :alt="item.person.name">
                    <div class="cInfo">
                        <h3>{{item.person.name}}</h3>
                        <h3>{{item.language}}</h3>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>
<script>
import { ref, onMounted } from "vue";
import { useRoute } from "vue-router";

export default {
    name: 'AboutCharacter',
    setup(props) {
        const characterInfo = ref([])
        const route = useRoute()
        const anime = ref([])
        const imageURL = ref('')
        const manga = ref([])
        const voices = ref([])
        const bestAnime = ref('')
        
        onMounted(() => {
            fetch(`https://api.jikan.moe/v4/characters/${route.params.id}/full`)
            .then(response => response.json())
            .then(data => {
                characterInfo.value = data.data
                anime.value = data.data.anime
                imageURL.value = data.data.images.webp.image_url
                manga.value = data.data.manga
                voices.value = data.data.voices
                bestAnime.value = anime.value[0].anime.title

                console.log(bestAnime.value)
                console.log(characterInfo.value)
            })
        })
        return {
            characterInfo,
            anime,
            imageURL,
            manga,
            voices,
            bestAnime
        }
    }
}
</script>
<style scoped>
    .charas {
        color: #fff;
        margin-top: 1rem;
        margin-bottom: 1rem;
    }
    .cIntro {
        display: flex;
        align-items: center;
    }
    .cIntro img {
        max-width: 200px;
        max-height: 250px;
        width: 100%;
        height: 100%;
        object-fit: cover;
        border-radius: 1.5rem;
    }
    .cIntroName {
        padding: 2rem;

    }
    .cAbout {
        margin: 1rem 0;
    }
    .cAbout h3 {
        margin-bottom: 0.5rem;
    }
    .cAbout p {
        color: #e0e0e0;
    }
    .cAnime, .cManga {
        margin: 2rem 0;
    }
    .cAnime h2, .cManga h2 {
        font-size: 17px;
        margin-bottom: 1rem;
    }
    .cAnimeList, .cMangaList {
        overflow: hidden;
        display: grid;
        gap: 1rem;
        grid-template-columns: repeat(auto-fit, minmax(11rem, 1fr));
    }
    .cAnimeList img, .cMangaList img {
        width: 100%;
        height: 250px;
        object-fit: cover;
        border-radius: 1rem;
    }
    .cAnimeList div, .cMangaList div {
        position: relative;
    }
    .cAnimeList .mini , .cMangaList .mini {
        text-align: center;
        font-size: 12px;
        padding: 0.5rem;
        background-image: linear-gradient(to top, rgba(0, 0, 0, 1), rgba(0, 0, 0, .3));
        border-radius: 1rem;
        border-bottom: 2px solid #1d1d1d;
        position: absolute;
        bottom: 0;
        left: 0;
        right: 0;
    }
    .mini h3:nth-child(1) {
        display: -webkit-box;
        overflow: hidden;
        -webkit-line-clamp: 2;
        -line-clamp: 2;
        -webkit-box-orient: vertical;
    }
    .mini h3:nth-child(2) {
        background-color: #fff;
        color: #000;
        padding: 0.3rem 0.5rem;
        width: fit-content;
        border-radius: 0.5rem;
        margin: .3rem auto;
    }
    .cVoice {
        margin: 2rem 0;
    }
    .cVoice h1 {
        font-size: 17px;
    }
    .cVoices {
        display: flex;
        flex-direction: row;
        flex-wrap: nowrap;
        overflow-x: auto;
    }
    .cVoices::-webkit-scrollbar {
        display: none;
    }
    .cVoice .man {
        margin: 1rem 0;
        margin-right: 1rem;
    }
    .cVoices img {
        width: 150px;
        height: 150px;
        object-fit: cover;
        border-radius: 50%;
    }
    .cInfo {
        font-size: 12px;
        color: #e0e0e0;
        text-align: center;
    }
    .cInfo h3:nth-child(2) {
        width: fit-content;
        padding: 0.3rem 0.5rem;
        border-radius: 0.5rem;
        background-color: #fff;
        color: #000;
        margin: auto;
    }
</style>