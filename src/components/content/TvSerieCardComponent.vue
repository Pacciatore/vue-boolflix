<template>
    <div>

        <div class="title">Titolo: {{tv.name}}</div>
        <div class="title">Titolo originale: {{tv.original_name}}</div>
        <div class="title">Lingua originale: <span><img :src="getLanguageFlag(tv)" :alt="tv.original_language"></span>
        </div>
        <div class="title">Voto: {{tv.vote_average}}</div>

    </div>
</template>

<script>
export default {
    name: 'TvSerieCardComponent',
    props: {
        tv: Object
    },
    methods: {
        getLanguageFlag(result) {
            let langFlag = "";
            // Controllo i casi in cui il codice lingua non coincide col codice bandiera
            switch (result.original_language) {
                case "ja":
                    langFlag = "jp";
                    break;
                case "en":
                    langFlag = "gb-eng";
                    break;
                case "cs":
                    langFlag = "cz";
                    break;
                case "da":
                    langFlag = "dk";
                    break;
                // Lingue indiane: hindi, telugu
                case "hi", "te":
                    langFlag = "in";
                    break;
                default:
                    langFlag = result.original_language;
                    break;
            }
            // Attribuisco il codice bandiera esatto e restituisco l'url
            const flagUrl = `https://flagcdn.com/16x12/${langFlag}.png`;
            return flagUrl;
        }
    }
}
</script>

<style lang="scss" scoped>

</style>