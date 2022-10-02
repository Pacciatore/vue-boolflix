<template>
    <header class="pt-4 pb-1">

        <div class="container d-flex justify-content-between align-items-center">

            <h1 class="brand-name text-uppercase">Boolflix</h1>

            <SearchComponent class="col-2" @search="getSearchText" />

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

    .brand-name {
        color: $tr-brand-color;
    }

}
</style>