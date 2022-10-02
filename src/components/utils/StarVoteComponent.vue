<template>
    <div class="d-flex">

        <font-awesome-icon icon="fa-solid fa-star" />

        <font-awesome-icon v-if="voteMaxFive > 1" icon="fa-solid fa-star" />

        <font-awesome-icon v-if="voteMaxFive > 2" icon="fa-solid fa-star" />

        <font-awesome-icon v-if="voteMaxFive > 3" icon="fa-solid fa-star" />

        <font-awesome-icon v-if="voteMaxFive > 4" icon="fa-solid fa-star" />

    </div>
</template>

<script>
export default {
    name: 'StarVoteComponent',
    data() {
        return {
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
            this.voteMaxFive = Math.ceil(this.vote / 2);
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