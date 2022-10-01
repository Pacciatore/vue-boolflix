<template>
  <main>

    <!-- Utilizzo di un componente per la ricerca -->
    <div class="container py-5">
      <SearchComponent @search="getSearchText" />
    </div>

    <LoaderComponent v-if="loading" />

    <!-- Elenco film risultato chiamata axios -->
    <div v-else class="container d-flex">
      <div class="movies col-5">
        <h2>Film</h2>
        <MovieCardComponent v-for="movie in movies" :key="movie.id" :movie="movie" />
      </div>

      <div class="tv-series col-5">
        <h2>Serie TV</h2>
        <TvSerieCardComponent v-for="tvSerie in tvSeries" :key="tvSerie.id" :tv="tvSerie" />
      </div>

    </div>

  </main>
</template>

<script>
import SearchComponent from '@/components/utils/SearchComponent.vue';
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
    getSearchTitle() {
      console.log("Ricerca su: ", this.inputText);
      this.$emit("search", this.inputText);
    },
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
    },
    getSearchText(textToSearch) {
      console.log("Nel main ottengo: ", textToSearch);
      this.$emit("search", textToSearch);
    }
  },
  components: {
    SearchComponent,
    LoaderComponent,
    TvSerieCardComponent,
    MovieCardComponent
  }
}
</script>

<style scoped lang="scss">
@import '@/assets/style/variables.scss';

main {
  background-color: $tr-bg-mockup;
  color: white;
}
</style>
