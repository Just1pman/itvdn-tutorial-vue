<template>
    <div>
        <character-block v-if="character" :character="character"/>
        <button @click="goBack">go back</button>
    </div>
</template>

<script>
import CharacterBlock from "@/components/CharacterBlock";

export default {
    name: "rick-and-morty-character",
    components: {
        CharacterBlock,
    },
    methods: {
        goBack() {
            this.$router.push({name: 'RickAndMortyList'});
        }
    },
    data() {
        return {
            character: null,
        }
    },
    async created() {
        try {
            const {id} = this.$route.params;
            console.log(id)
            if (id) {
                const {data} = await this.$store.dispatch('fetchSingleCharacter', id);
                this.character = data;
            }
        } catch (err) {
           console.log(err);
        }
    }
}

</script>

<style scoped>

</style>