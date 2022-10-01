<template>
    <div>

        <img :src="getPosterPath()" :alt="posterName">

    </div>
</template>

<script>
export default {
    name: 'PosterComponent',
    data() {
        return {
            posterPath: '',
            posterWidth: 'w342'
        }
    },
    props: {
        posterEndPath: String,
        posterName: String
    },
    methods: {
        getPosterPath() {
            return this.posterPath = `https://image.tmdb.org/t/p/${this.posterWidth}/${this.posterEndPath}`;
        }
    }
}
</script>

<style lang="scss" scoped>

</style>