<template>
    <article class="character-block">
        <div class="character-block__image">
            <img :src="character.image" :alt="character.name">
        </div>
        <div class="character-block__info">
            <h2 class="character-block__info--name" @click="detailedInfo">{{character.name}}</h2>
            <span class="character-block__info--status"><span class="status__icon"></span> {{character.status}} - {{character.species}}</span>
            <p class="character-block__info--location">
                <span>Last know location:</span>
                {{character.location.name}}
            </p>
        </div>
    </article>
</template>

<script>
export default {
    name: "CharacterBlock",
    props: {
        character: {
            type: Object,
            required: true
        }
    },
    data() {
        return {}
    },
    created() {
        this.$store.dispatch("fetchCharacters", 1);
    },
    mounted() {

    },

    methods: {
        detailedInfo () {
            this.$router.push({ name:'CharacterDetails', params: {id: this.character.id} })
        }
    }
}
</script>

<style scoped>
.character-block__info {
    font-size: 1.5rem;
}

</style>