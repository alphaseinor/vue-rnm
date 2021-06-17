<template>
    <article>
        <h2>{{character.name}}</h2>
        <img :src="`${character.image}`" :alt="`${character.name}`">
        <p>{{character.name}} is a {{character.gender}} {{character.species}}</p>
        <p>Who's status is {{character.status}}</p>
        <p>{{character.name}} is originally from {{character.origin.name}} and is currently in {{character.location.name}}</p>
        <h3>Episodes {{character.name}} is in:</h3>
        <div>
            <CharacterEpisode v-bind:episode="episode" v-for="episode in episodes" v-bind:key="episode.id" />
        </div>
    </article>
</template>

<script>
import axios from 'axios'
import CharacterEpisode from './CharacterEpisode.vue'

export default {
    name: "Character",
    props: ["character"],
    data() {
        return {
            episodes: []
        }
    },
    components: {
        CharacterEpisode
    },
    created() {
        this.character.episode.forEach(episode => {
            axios.get(episode)
             .then(({data}) => {
                 //pasrse the seasons and episodes, then add episodes to local state
                 const [season, episode] = data.episode.split("S")[1].split("E")
                 this.episodes = [...this.episodes, {
                    name: data.name,
                    air_date: data.air_date,
                    season, 
                    episode,
                    url: data.url,
                    id: data.id
                }]
             })
        })
    }

}
</script>

<style scoped>

</style>