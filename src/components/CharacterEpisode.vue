<template>
    <aside>
        <h3>Season {{episode.season}} episode {{episode.episode}}:{{episode.name}}</h3>
        <p>OAir Date: {{episode.air_date}}</p>
    </aside>
</template>

<script>
export default {
    name: "CharacterEpisode",
    props: ["episode"]
}
</script>

<style scoped>

</style>