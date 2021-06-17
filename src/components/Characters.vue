<template>
    <section>
        <article v-bind:key="character.id" v-for="character in characters">
            <Character v-bind:character="character" />
        </article>
    </section>
</template>

<script>
import Character from './Character.vue'
import axios from 'axios'

export default {
    name: "Characters",
    data() {
        return {
            characters: [],
            characterNum: 0,
            endpoint: "/character/",
            parsedURL: "",
            currentPage: 1,
            totalPages: 0,
            name: "",
            gender: "",
            status: "",
            types: [],
            selectedType: "",
            tempParse: []
        }
    },
    props: ["baseURL"],
    components: {
        Character
    },
    methods: {
        
    },
    created() {
        const parseURL = () => {
    
            // figure out if we need a ? or a &
            const qOrA = () => {
                return this.tempParse.length > 2 ? "&" : "?"
            }
            
            // concatenate our baseURL with our endpoint
            this.tempParse = [this.baseURL, this.endpoint]
    
            // adds page to the list if more than 1
            if (this.currentPage > 1){
                this.tempParse = [...this.tempParse, qOrA(), "page=", this.currentPage]
            }
    
            // adds name to the list if not empty
            if (this.name !== ""){
                this.tempParse = [...this.tempParse, qOrA(), "name=", this.name]
            }
    
            if (this.gender !== ""){
                this.tempParse = [...this.tempParse, qOrA(), "gender=", this.gender]
            }
    
            if (this.status !== ""){
                this.tempParse = [...this.tempParse, qOrA(), "status=", this.status]
            }

            if (this.type !== ""){
                this.tempParse = [...this.tempParse, qOrA(), "type=", this.selectedType]
            }

            //stringify the array
            this.parsedURL = this.tempParse.join("")
        }
        
        parseURL()
        // `${this.baseURL}${this.endpoint}?page=${this.currentPage}&${this.name !== "" && `name=${this.name}`}&$gender=${this.gender}&status=${status}&type=${this.selectedType}`
        axios.get(this.parsedURL)
        .then(({data}) => {
            this.characters = data.results
            this.totalPages = data.info.pages
            this.characterNum = data.info.count
            this.data.results.forEach(character => {
                if(character.type !== ""){
                    this.types = [...this.types, character]
                }
            })
        })
    }
}

</script>

<style scoped>

</style>