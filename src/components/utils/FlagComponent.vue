<template>
    <span>

        <img v-if="!loadError" @error="loadError = true" :src="getLanguageFlag(nationality)" :alt="nationality">

        <span v-else>{{nationality}}</span>

    </span>
</template>

<script>
export default {
    name: 'FlagComponent',
    data() {
        return {
            loadError: false
        }
    },
    props: {
        nationality: String
    },
    methods: {
        getLanguageFlag(nationality) {
            let langFlag = "";
            // Controllo i casi in cui il codice lingua non coincide col codice bandiera
            switch (nationality) {
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
                case "hi":
                    langFlag = "in";
                    break;
                case "te":
                    langFlag = "in";
                    break;
                default:
                    langFlag = nationality;
                    break;
            }
            // Attribuisco il codice bandiera esatto e restituisco l'url
            const flagUrl = `https://flagcdn.com/h20/${langFlag}.png`;
            return flagUrl;
        }
    }

}
</script>

<style lang="scss" scoped>

</style>