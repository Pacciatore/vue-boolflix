<template>
    <header>

        <!-- Utilizzo di un componente per la ricerca -->
        <div class="container py-5">
            <SearchComponent @search="getSearchText" />
        </div>

    </header>
</template>

<script>
import SearchComponent from '@/components/utils/SearchComponent.vue';

export default {
    name: 'HeaderComponent',
    methods: {
        getSearchText(textToSearch) {
            console.log("Nel main ottengo: ", textToSearch);
            this.$emit("search", textToSearch);
        }
    },
    components: {
        SearchComponent
    }
}
</script>

<style lang="scss" scoped>
@import '@/assets/style/variables.scss';

header {
    background-color: $tr-header-bg;
}
</style>