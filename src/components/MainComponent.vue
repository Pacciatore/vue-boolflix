<template>
  <main class="container py-5">


    <!-- Elenco film risultato chiamata axios -->
    <div class="results-container d-flex flex-column justify-content-center">

      <div class="movies col d-flex flex-column">
        <h2 class="col-12">Film</h2>

        <LoaderComponent v-if="loading" />

        <div v-else class="card-container d-flex gap-5">
          <MovieCardComponent class="card-element flex-shrink-0" v-for="movie in movies" :key="movie.id"
            :movie="movie" />
        </div>

      </div>

      <div class="tv-series pt-5 col d-flex flex-column">
        <h2 class="col-12">Serie TV</h2>

        <LoaderComponent v-if="loading" />

        <div v-else class="card-container d-flex gap-5">
          <TvSerieCardComponent class="card-element flex-shrink-0" v-for="tvSerie in tvSeries" :key="tvSerie.id"
            :tv="tvSerie" />
        </div>

      </div>

    </div>

  </main>
</template>

<script>
import LoaderComponent from '@/components/utils/LoaderComponent.vue';

import TvSerieCardComponent from '@/components/content/TvSerieCardComponent.vue';
import MovieCardComponent from '@/components/content/MovieCardComponent.vue';


export default {
  name: "MainComponent",
  data() {
    return {
      inputText: ""
    };
  },
  props: {
    movies: Array,
    tvSeries: Array,
    loading: Boolean
  },
  methods: {
    getLanguageFlag(result) {
      let langFlag = "";
      // Controllo i casi in cui il codice lingua non coincide col codice bandiera
      switch (result.original_language) {
        case "ja":
          langFlag = "jp";
          break;
        case "en":
          langFlag = "gb-eng";
          break;
        case "cs":
          langFlag = "cz";
          break;
        case "da":
          langFlag = "dk";
          break;
        // Lingue indiane: hindi, telugu
        case "hi", "te":
          langFlag = "in";
          break;
        default:
          langFlag = result.original_language;
          break;
      }
      // Attribuisco il codice bandiera esatto e restituisco l'url
      const flagUrl = `https://flagcdn.com/16x12/${langFlag}.png`;
      return flagUrl;
    }
  },
  components: {
    LoaderComponent,
    TvSerieCardComponent,
    MovieCardComponent
  }
}
</script>

<style scoped lang="scss">
.movies,
.tv-series {
  min-height: 532px;
}

.card-container {

  overflow-x: auto;

  &::-webkit-scrollbar {
    // TODO: aggiungere un pulsante per lo scorrimento

    // display: none;
  }

  .card-element {
    width: 344px;
  }
}
</style>
