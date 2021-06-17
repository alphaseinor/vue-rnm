/*
    Outputs
        component containing buttons or other links that emit page-number 

    Inputs (props)
        required: currentPage, numberOfPages
        currentPage is the page number that the user is on, this will return a class of "disabled"
        numberOfPages is 1 to number of pages inclusive. 

    Constraints
        returns a div with anchor tags, clicking the anchor tag will emit that anchor tag number. 

    Edge cases
        1 and last page
        returns page 1 if request is lower than 1
        last page if request is higher
 */
