<template>
    <div>
        <div class="results">
            <h3 class="hResults">Did you search for {{ text }}?</h3>
            <div class="rList">
            <router-link :to="'/about/'+anime.mal_id" v-for="anime in foundAnime" :key="anime.mal_id">
                <img :src="anime.images.webp.image_url" :alt="anime.title">
                <div class="foundInfo">
                <h3>{{ anime.title_english }}</h3>
                </div>
            </router-link>
            </div>
        </div>
    </div>
</template>

<script>
import { ref, defineProps, onBeforeMount } from "vue";

export default {
    name: 'SearchAnime',
    props: {
        text: {
            type: String,
            required: true
        }
    },
    watch: {
        text(newValue, oldValue) {
            this.refreshView()
        }
    },
    methods: {
        refreshView() {
            this.text = this.text
        }
    },
    setup(props) {
        const foundAnime = ref([])
        const resultsHeading = ref('')
        // const gotText = 'text'
        onBeforeMount(() => {
            fetch(`https://api.jikan.moe/v4/anime?q=${props.text}`)
            .then(res => res.json())
            .then(data => {
                // console.log(data)
                foundAnime.value = data.data
            })
        })


        return {
            foundAnime,
            // gotText,
            text: props.text
        }
    }
}
</script>

<style>
    
</style>