<template>
    <div class="card position-relative rounded-0">

        <PosterComponent :posterEndPath="tv.poster_path" :posterName="tv.original_name" />

        <div class="tv-info position-absolute h-100 w-100 py-5 px-3">

            <div class="info-element">
                <span class="fw-bold pe-1">Titolo:</span> <span>{{tv.name}}</span>
            </div>

            <div class="info-element">
                <span class="fw-bold pe-1">Titolo originale:</span> <span>{{tv.original_name}}</span>
            </div>

            <div class="info-element">
                <span class="fw-bold pe-1">Lingua originale:</span>
                <FlagComponent :nationality="tv.original_language" />
            </div>

            <div class="info-element">
                <span class="fw-bold pe-1">Voto:</span>
                <StarVoteComponent :vote="tv.vote_average" />
            </div>

            <div class="info-element">
                <span class="fw-bold pe-1">Descrizione:</span>
                <span v-if="tv.overview.length === 0">Descrizione non disponibile</span>
                <span v-else>{{tv.overview}}</span>
            </div>

        </div>

    </div>
</template>

<script>
import FlagComponent from '@/components/utils/FlagComponent.vue';
import PosterComponent from '@/components/utils/PosterComponent.vue';
import StarVoteComponent from '@/components/utils/StarVoteComponent.vue';

export default {
    name: "TvSerieCardComponent",
    props: {
        tv: Object
    },
    components: {
        FlagComponent,
        PosterComponent,
        StarVoteComponent
    }
}
</script>

<style lang="scss" scoped>
.tv-info {
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