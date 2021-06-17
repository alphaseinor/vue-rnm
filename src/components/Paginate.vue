/*
    Outputs
        component containing buttons or other links that emit page-number 

    Inputs (props)
        required: currentPage, totalPages
        currentPage is the page number that the user is on, this will return a class of "disabled"
        totalPages is 1 to number of pages inclusive. 

    Constraints
        returns a div with anchor tags, clicking the anchor tag will emit that anchor tag number. 

    Edge cases
        1 and last page
        returns page 1 if request is lower than 1
        last page if request is higher
 */

 <template>
     <div class="paginate-list">

     </div>
 </template>
<script>
export default {
    name: "Paginate",
    props: ["currentPage","totalPages"],
    data() {
        return {
            pageArray: this.arrayGen()
        }
    },
    methods: {
        arrayGen(){
            let pageArray = []
            for(let i = 0; i < this.totalPages; i++){
                pageArray = [...pageArray, i + 1]
            }
            console.log(pageArray)
            return pageArray
        }
    }
}
</script>