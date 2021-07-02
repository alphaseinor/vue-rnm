<template>
    <main>
        <section>
            <Paginate v-on:changePage="changePage" :currentPage="currentPage" :totalPages="totalPages" :pageArray="pageArray"/>
        </section>
        <section class="flex flex-wrap justify-evenly">
            <article class="border-solid p-4ß" style="width:300px;" v-bind:key="character.id" v-for="character in characters">
                <Character v-bind:character="character" />
            </article>
        </section>
    </main>
</template>

<script>
import Character from './Character.vue'
import Paginate from './Paginate.vue'
import axios from 'axios'

export default {
    name: "Characters",
    data() {
        return {
            characters: [],
            characterNum: 0,
            endpoint: "/character/",
            currentPage: 1,
            totalPages: 0,
            name: "",
            gender: "",
            status: "",
            types: [],
            selectedType: "",
            pageArray: []
        }
    },
    props: ["baseURL"],
    components: {
        Character,
        Paginate
    },
    methods: {
        changePage(newPage){
            this.currentPage = newPage
            this.getData()
        },
        parseURL(){
            let tempParse = []
            // figure out if we need a ? or a &
            const qOrA = () => {
                return tempParse.length > 2 ? "&" : "?"
            }
            
            // concatenate our baseURL with our endpoint
            tempParse = [this.baseURL, this.endpoint]
    
            // adds page to the list if more than 1
            if (this.currentPage > 1){
                tempParse = [...tempParse, qOrA(), "page=", this.currentPage]
            }
    
            // adds name to the list if not empty
            if (this.name !== ""){
                tempParse = [...tempParse, qOrA(), "name=", this.name]
            }
    
            if (this.gender !== ""){
                tempParse = [...tempParse, qOrA(), "gender=", this.gender]
            }
    
            if (this.status !== ""){
                tempParse = [...tempParse, qOrA(), "status=", this.status]
            }

            if (this.type !== ""){
                tempParse = [...tempParse, qOrA(), "type=", this.selectedType]
            }

            //stringify the array
            return tempParse.join("")
        },
        getData(){
            axios.get(this.parseURL())
                .then(({data}) => {
                    this.characters = data.results
                    this.totalPages = data.info.pages
                    this.pageArray = Array.from({length: data.info.pages}, (v, i) => i+1)
                    this.characterNum = data.info.count
                    data.results.forEach(character => {
                        if(character.type !== ""){
                            this.types = [...this.types, character]
                        }
                    })
    
                })
        }
    },
    created() {
        this.getData()
    }
}

</script>

<style scoped>

</style>