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
     <div class="paginate-list">
        <button v-bind:disabled="start">Previous</button>
        <button :key="page" v-for="page in pageArray" :class="currentpage == page && 'current'" >{{page}}</button>
         <button v-bind:disabled="end">Next</button>
     </div>
 </template>
<script>

export default {
    name: "Paginate",
    props: ["currentPage","totalPages", "pageArray"],
    data() {
        return {
            computedPage: 1,
            start: false,
            end: false
        }
    },
    methods: {
        checkStart(){
            if(this.currentPage <= 1){
                this.computedPage = 1
                this.start = true
            }
        },
        checkEnd(){
            if(this.currentPage >= this.totalPages ){
                this.computedPage = this.pageArray.length
                this.end = true;
            }
        },
        
    },
    computed: {
    },
    created(){
        this.computedPage = this.currentPage
        this.arrayFinished = true
        this.checkStart()
        this.checkEnd()
    }
}
</script>