<template>
    <div class="card position-relative rounded-0">

        <PosterComponent :posterEndPath="movie.poster_path" :posterName="movie.original_title" />

        <div class="movie-info position-absolute h-100 w-100 py-5 px-3">

            <div class="info-element">
                <span class="fw-bold pe-1">Titolo:</span> <span>{{movie.title}}</span>
            </div>

            <div class="info-element">
                <span class="fw-bold pe-1">Titolo originale:</span> <span>{{movie.original_title}}</span>
            </div>

            <div class="info-element">
                <span class="fw-bold pe-1">Lingua originale:</span>
                <FlagComponent :nationality="movie.original_language" />
            </div>

            <div class="info-element">
                <span class="fw-bold pe-1">Voto:</span>
                <StarVoteComponent :vote="movie.vote_average" />
            </div>

            <div class="info-element">
                <span class="fw-bold pe-1">Descrizione:</span>
                <span v-if="movie.overview.length === 0">Descrizione non disponibile</span>
                <span v-else>{{movie.overview}}</span>
            </div>

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
.movie-info {
    opacity: 0;
    top: 0;
    background-color: black;

    transition: all 0.1s;

    overflow-y: auto;

    &::-webkit-scrollbar {
        display: none;
    }

    &:hover {
        opacity: 1;
        cursor: default;
    }

    .info-element {
        *:nth-child(2) {
            color: #ffffffe0;
        }
    }

}
</style>