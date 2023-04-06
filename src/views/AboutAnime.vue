<template>
    <div>
        <h3>{{ $route.params.id }}</h3>
    </div>
</template>

<script>
    import { ref, onBeforeMount } from "vue";
    import { useRoute } from "vue-router";

    export default {
        name: 'AboutAnime',

        setup() {
            const animeDetails = ref([])
            const route = useRoute()

            onBeforeMount(() => {
                fetch(`https://api.jikan.moe/v4/anime/${route.params.id}/full`)
                .then(res => res.json())
                .then(data => {
                    console.log(data)
                })
            })
            return {
                route
            }
        }
    }
</script>
