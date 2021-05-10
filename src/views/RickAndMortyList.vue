<template>
    <div class="home">
        <h1 class="home-title">The Rick and Morty</h1>
        <div class="content">
            <div class="character-list">
                <character-block
                    v-for="character in characters"
                    :key="character.id"
                    :character="character"
                />
            </div>
            <paginate
                v-if="pages"
                v-model="currentPage"
                :page-count="pages"
                :page-range="2"
                :margin-pages="2"
                :click-handler="clickCallback"
                :prev-text="'Prev'"
                :next-text="'Next'"
                :prev-class="'page-item'"
                :next-class="'page-item'"
                :container-class="'pagination'"
                :page-class="'page-item'">
            </paginate>
        </div>
    </div>
</template>

<script>
import CharacterBlock from "@/components/CharacterBlock";

const Paginate = () => import('vuejs-paginate');

export default {
    name: 'rick-and-morty-list',
    components: {
        CharacterBlock,
        Paginate
    },
    data() {
        return {
            currentPage: 1
        }
    },
    created() {
        this.$store.dispatch('fetchCharacters', this.currentPage);
    },
    methods: {
        clickCallback: function (pageNum) {
            this.currentPage = pageNum;
        },
    },
    watch: {
        currentPage: {
            handler(page) {
                console.log(page, 'page change');
                this.$store.dispatch('fetchCharacters', page)
            }
        }
    },
    computed: {
        characters() {
            return this.$store.getters['getCharactersByPage'](this.currentPage);
        },
        firstCharacter() {
            return this.$store.getters['getCharactersById']({id: 1, page: 1});
        },
        pages() {
            return this.$store.state.pages;
        }
    }
}
</script>
