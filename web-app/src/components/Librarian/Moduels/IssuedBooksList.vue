<template>
    <div> 
        <BookList 
            v-bind:title='this.title'
            v-bind:bookList='this.issuedBooks'
            v-bind:limit='9'>
        </BookList> 
    </div>
</template>

<script>
import BookList from '../../SharedModules/BookList'

export default {
    name: 'IssuedBooksList',

    components: {
        BookList
    },

    props:{
        showStock: {
            type: Boolean,
            default: true
        }
    },

    data() {
        return {
            title: "Issued Books",
            issuedBooks: []
        }
    },
    
    mounted() {
        this.fetchIssuedBooks()
    },

    methods: {
        fetchIssuedBooks: function() {
            fetch('http://127.0.0.1:5000/books/issued/all')
            .then(res => res.json())
            .then((data) => {
                var books = data['issued_books']
                console.log(books)
                for(let i = 0; i < books.length; i++) {
                    let book = books[i]
                    var issuedBook = {}
                    issuedBook['imgSrc'] = book['book_detail']['img_src']
                    this.issuedBooks.push(issuedBook)
                }
            })
            .catch(err => console.log(err.message))
        }
    },    
}
</script>

<style>

</style>