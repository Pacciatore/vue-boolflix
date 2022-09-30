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
        <div class="title">Lingua originale: {{result.original_language}}</div>
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
    }
  }
}
</script>

<style scoped lang="scss">

</style>
