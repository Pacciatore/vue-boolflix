<template>
  <div id="app">

    <MainComponent :apiResults="results" @search="getFilms" />

  </div>
</template>

<script>
// Libraries import
import 'bootstrap/dist/css/bootstrap.css';
import axios from 'axios';

import MainComponent from '@/components/MainComponent.vue';

export default {
  name: 'App',
  data() {
    return {
      moviesApiUrl: 'https://api.themoviedb.org/3/',
      myApiKey: '0b6447f7bfd63c42725507a256906e8f',

      results: []
    }
  },
  created() {
    this.getApiResource();
  },
  methods: {

    // Tutorial personale
    getApiResource() {
      axios.get(`${this.moviesApiUrl}search/movie?api_key=${this.myApiKey}&query=lego`)
        .then(({ status, data }) => {
          console.log(status, data)
          this.results = data.results;
        })
        .catch((e) => {
          console.log(e)
        })
    },

    getFilms(textToSearch) {

      axios.get(`${this.moviesApiUrl}search/movie?api_key=${this.myApiKey}&query=${textToSearch}`)
        .then(({ status, data }) => {
          console.log(status, data)
          this.results = data.results;
        })
        .catch((e) => {
          console.log(e)
        })


    }

  },
  components: {
    MainComponent
  }
}
</script>

<style lang="scss">
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
</style>
