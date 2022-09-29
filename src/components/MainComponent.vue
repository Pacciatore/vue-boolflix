<template>
  <div class="container pt-5">

    <div class="search-area">
      <input type="text">
      <button>Cerca</button>
    </div>

    <!-- Elenco film risultato chiamata axios -->
    <ul>
      <li v-for="result in apiResults" :key="result.id">
        {{result.title}}
      </li>
    </ul>

  </div>
</template>

<script>
export default {
  name: 'MainComponent',
  props: {
    apiResults: Array
  }
}
</script>

<style scoped lang="scss">

</style>
