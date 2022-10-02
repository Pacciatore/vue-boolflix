<template>
    <div>

        <PosterComponent :posterEndPath="movie.poster_path" :posterName="movie.original_title" />

        <div class="title">Titolo: {{movie.title}}</div>
        <div class="title">Titolo originale: {{movie.original_title}}</div>
        <div class="title">Lingua originale:
            <FlagComponent :nationality="movie.original_language" />
        </div>
        <div class="title">Voto:
            <StarVoteComponent :vote="movie.vote_average" />
        </div>

    </div>
</template>

<script>
import FlagComponent from '@/components/utils/FlagComponent.vue';
import PosterComponent from '@/components/utils/PosterComponent.vue';
import StarVoteComponent from '@/components/utils/StarVoteComponent.vue';

export default {
    name: "MovieCardComponent",
    props: {
        movie: Object
    },
    components: {
        FlagComponent,
        PosterComponent,
        StarVoteComponent
    }
}
</script>

<style lang="scss" scoped>

</style>