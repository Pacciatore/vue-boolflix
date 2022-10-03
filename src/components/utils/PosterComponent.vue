<template>
    <div>

        <img :src="getPosterPath()" :alt="posterName" @error="setUnavailablePoster($event)">

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
        },
        setUnavailablePoster(event) {
            event.target.src = 'https://www.metrorollerdoors.com.au/wp-content/uploads/2018/02/unavailable-image-300x225.jpg'
        }
    }
}
</script>

<style lang="scss" scoped>
img {
    width: 342px;
}
</style>