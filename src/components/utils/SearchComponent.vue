<template>
    <div class="search-area">
        <input type="text" placeholder="Inserire elemento da cercare" v-model="inputText" @keyup.enter="getSearchTitle">
        <button @click="getSearchTitle">Cerca</button>
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