<template>
    <div>
        <div class="results">
            <h3 class="hResults"></h3>
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
export default {
    name: 'SearchAnime'
}
</script>
<style>
    
</style>