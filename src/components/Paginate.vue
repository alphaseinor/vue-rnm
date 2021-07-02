/*
    Outputs
        component containing buttons or other links that emit page-number 

    Inputs (props)
        required: currentPage, totalPages, pageArray
        currentPage: page number that the user is on, this will return a class of "disabled"
        pageArray: a simple array like this.pageArray = Array.from({length: data.info.pages}, (v, i) => i+1) passed from parent. this will be generated at the time of GET. 

    Constraints
        returns a div with anchor tags, clicking the anchor tag will emit that anchor tag number. 

    Edge cases
        1 and last page
        returns page 1 if request is lower than 1
        last page if request is higher
 */

 <template>
     <div class="flex flex-wrap justify-center">
        <button class="p-2" @click="$emit('changePage', currentPage - 1)" v-bind:disabled="checkStart">Previous</button>
        <button class="p-2" @click="$emit('changePage', page)" :key="page" v-for="page in pageArray" :class="currentPage == page && 'current'" >{{page}}</button>
         <button class="p-2" @click="$emit('changePage', currentPage + 1)" v-bind:disabled="checkEnd">Next</button>
     </div>
 </template>
<script>

export default {
    name: "Paginate",
    props: ["currentPage","totalPages", "pageArray"],
    computed: {
        checkStart(){
            let isTrue = true
            if(this.currentPage > 1){
                isTrue = false
            }
            return isTrue
        },
        checkEnd(){
            let isTrue = true
            if(this.currentPage < this.totalPages ){
                isTrue = false
            }
            return isTrue
        },
        checkSamePage(page){
            let isTrue = true
            if(this.currentPage == page ){
                isTrue = false
            }
            return isTrue
        }
    },
}
</script>

<style scoped>
    .current{
        border: 2px solid purple;
        background: none;
        font-weight: bolder;
    }
</style>