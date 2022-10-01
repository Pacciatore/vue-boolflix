<template>
  <div id="app">

    <MainComponent :loading="loading" v-if="errorMessage.length === 0" :apiResults="results" @search="search" />
    <div v-else>{{ errorMessage }}</div>


  </div>
</template>

<script>
// Libraries import
import 'bootstrap/dist/css/bootstrap.css';
import axios from 'axios';

import { apiKey } from '@/env'

import MainComponent from '@/components/MainComponent.vue';

export default {
  name: 'App',
  data() {
    return {
      apiUrl: 'https://api.themoviedb.org/3/',

      results: [],

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
          this.results = this.getDataFromApiResponse(response);
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
