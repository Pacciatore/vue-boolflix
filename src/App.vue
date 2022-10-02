<template>
  <div id="app">

    <HeaderComponent @search="search" />

    <MainComponent :loading="loading" v-if="errorMessage.length === 0" :tvSeries="tvSeries" :movies="movies" />
    <div v-else>{{ errorMessage }}</div>


  </div>
</template>

<script>
// Libraries import
import 'bootstrap/dist/css/bootstrap.css';
import axios from 'axios';

import { apiKey } from '@/env'

import MainComponent from '@/components/MainComponent.vue';
import HeaderComponent from './components/HeaderComponent.vue';

export default {
  name: 'App',
  data() {
    return {
      apiUrl: 'https://api.themoviedb.org/3/',

      movies: [],
      tvSeries: [],

      loading: false,
      errorMessage: ''
    }
  },
  methods: {
    // Slego la ricerca dalla chiamata API
    search(query) {
      this.queryApi(query)
    },

    queryApi(textToSearch) {

      this.loading = true;

      axios.get(`${this.apiUrl}search/movie?api_key=${apiKey}&query=${textToSearch}`)
        .then((response) => {
          this.loading = false;
          this.movies = this.getDataFromApiResponse(response);
        })
        .catch((e) => {
          this.loading = false;
          this.errorMessage = 'Error: ' + e.message;
          console.log(e)
        })

      axios.get(`${this.apiUrl}search/tv?api_key=${apiKey}&language=it_IT&query=${textToSearch}`)
        .then((response) => {
          this.loading = false;
          this.tvSeries = this.getDataFromApiResponse(response);
        })
        .catch((e) => {
          this.loading = false;
          this.errorMessage = 'Error: ' + e.message;
          console.log(e)
        })

    },

    getDataFromApiResponse(response) {
      console.log(response);
      return response.status === 200 ? response.data.results : []
    }

  },
  components: {
    MainComponent,
    HeaderComponent
  }
}
</script>

<style lang="scss">
@import '@/assets/style/variables.scss';

#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;

  height: 100vh;

  background-color: $tr-bg-mockup;
  color: white;

}
</style>
