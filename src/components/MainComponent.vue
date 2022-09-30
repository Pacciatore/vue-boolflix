<template>
  <div class="container pt-5">

    <div class="search-area">
      <input type="text" placeholder="Inserire titolo film" v-model="inputText" @keyup.enter="getSearchTitle">
      <button @click="getSearchTitle">Cerca</button>
    </div>

    <!-- Elenco film risultato chiamata axios -->
    <ul>
      <li v-for="result in apiResults" :key="result.id">
        <div class="title">Titolo: {{result.title}}</div>
        <div class="title">Titolo originale: {{result.original_title}}</div>
        <div class="title">Lingua originale: <span><img :src="getLanguageFlag(result)"
              :alt="result.original_language"></span></div>
        <div class="title">Voto: {{result.vote_average}}</div>
      </li>
    </ul>

  </div>
</template>

<script>
export default {
  name: 'MainComponent',
  data() {
    return {
      inputText: ''
    }
  },
  props: {
    apiResults: Array
  },
  methods: {
    getSearchTitle() {
      console.log('Ricerca su: ', this.inputText);
      this.$emit('search', this.inputText)
    },
    getLanguageFlag(result) {

      let langFlag = '';

      switch (result.original_language) {
        case 'ja':
          langFlag = 'jp'
          break;
        case 'en':
          langFlag = 'gb-eng'
          break;
        case 'cs':
          langFlag = 'cz'
          break;
        case 'da':
          langFlag = 'dk'
          break;
        // Lingue indiane: hindi, telugu
        case 'hi', 'te':
          langFlag = 'in'
          break;

        default:
          langFlag = result.original_language
          break;
      }


      const flagUrl = `https://flagcdn.com/16x12/${langFlag}.png`

      return flagUrl
    }
  }
}
</script>

<style scoped lang="scss">

</style>
