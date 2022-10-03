<template>
    <span>

        <font-awesome-icon v-for="index in max" :key="index" :icon="[
            index <= voteMaxFive ? 'fa-solid' : 'fa-regular',
            'fa-star'
        ]" />

    </span>
</template>

<script>
const MAX_STARS = 5;
const VOTE_BASE = 10;

export default {
    name: 'StarVoteComponent',
    data() {
        return {
            max: MAX_STARS,
            voteMaxFive: 1
        }
    },
    props: {
        vote: Number
    },
    created() {
        this.voteToMaxFive();
    },
    methods: {
        voteToMaxFive() {
            this.voteMaxFive = Math.ceil(this.vote / VOTE_BASE * MAX_STARS);
        }
    }
}
</script>

<style lang="scss" scoped>
@import '@/assets/style/variables.scss';

.fa-star {
    color: $tr-star-yellow;
}
</style>