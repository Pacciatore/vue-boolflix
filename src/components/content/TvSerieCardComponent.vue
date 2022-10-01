<template>
    <div>

        <PosterComponent :posterEndPath="tv.poster_path" :posterName="tv.original_name" />

        <div class="title">Titolo: {{tv.name}}</div>
        <div class="title">Titolo originale: {{tv.original_name}}</div>
        <div class="title">Lingua originale:
            <FlagComponent :nationality="tv.original_language" />
        </div>
        <div class="title">Voto: {{tv.vote_average}}</div>

    </div>
</template>

<script>
import FlagComponent from '@/components/utils/FlagComponent.vue';
import PosterComponent from '@/components/utils/PosterComponent.vue';

export default {
    name: "TvSerieCardComponent",
    props: {
        tv: Object
    },
    components: {
        FlagComponent,
        PosterComponent
    }
}
</script>

<style lang="scss" scoped>

</style>