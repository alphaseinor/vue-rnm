<template>
  <div id="app">
    <Characters v-bind:baseURL="baseURL"/>
  </div>
</template>

<script>

import Characters from './components/Characters.vue'

export default {
  name: 'App',
  data() {
    return {
      baseURL: 'https://rickandmortyapi.com/api'
    }
  },
  components: {
    Characters
  },
  methods: {

  }
}
</script>

<style>

</style>
