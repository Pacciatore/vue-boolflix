<template>
    <div class="search-area">

        <input class="w-100" type="text" placeholder="Inserire elemento da cercare" v-model="inputText"
            @keyup.enter="getSearchTitle">

        <!--         Eliminazione bottone di ricerca per questioni estetiche
        <button @click="getSearchTitle">Cerca</button> -->

    </div>
</template>

<script>
export default {
    name: 'SearchComponent',
    data() {
        return {
            inputText: ""
        };
    },
    methods: {

        getSearchTitle() {
            console.log("Ricerca su: ", this.inputText);
            this.$emit("search", this.inputText);
        },

    }
}
</script>

<style lang="scss" scoped>

</style>