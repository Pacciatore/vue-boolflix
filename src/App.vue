<template>
  <div id="app">

    <LoaderComponent v-if="loading" />
    <MainComponent v-else-if="errorMessage.length === 0" :apiResults="results" @search="getFilms" />
    <div v-else>{{ errorMessage }}</div>


  </div>
</template>

<script>
// Libraries import
import 'bootstrap/dist/css/bootstrap.css';
import axios from 'axios';

import MainComponent from '@/components/MainComponent.vue';
import LoaderComponent from '@/components/utils/LoaderComponent.vue';

export default {
  name: 'App',
  data() {
    return {
      moviesApiUrl: 'https://api.themoviedb.org/3/',
      myApiKey: '0b6447f7bfd63c42725507a256906e8f',

      results: [],

      loading: true,
      errorMessage: ''
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
          this.loading = false;
          if (status === 200) {
            console.log(status, data)
            this.results = data.results;
          }
          else {
            this.errorMessage = 'Something went wrong...'
          }
        })
        .catch((e) => {
          this.loading = false;
          this.errorMessage = 'Error: ' + e.message;
          console.log(e)
        })
    },

    getFilms(textToSearch) {

      this.loading = true;

      axios.get(`${this.moviesApiUrl}search/movie?api_key=${this.myApiKey}&query=${textToSearch}`)
        .then(({ status, data }) => {
          this.loading = false;
          if (status === 200) {
            console.log(status, data)
            this.results = data.results;
          }
          else {
            this.errorMessage = 'Something went wrong...'
          }
        })
        .catch((e) => {
          this.loading = false;
          this.errorMessage = 'Error: ' + e.message;
          console.log(e)
        })


    }

  },
  components: {
    MainComponent,
    LoaderComponent
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
