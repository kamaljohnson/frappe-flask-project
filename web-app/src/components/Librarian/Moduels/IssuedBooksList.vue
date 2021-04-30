<template>
    <div> 
        <BookList 
            v-bind:title='this.title'
            v-bind:bookList='this.issuedBooks'
            v-bind:limit='this.limit - 1'>
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
            issuedBooks: [],
            limit: 8
        }
    },
    
    mounted() {
        this.fetchIssuedBooks()
    },

    methods: {
        fetchIssuedBooks() {
            fetch('http://127.0.0.1:5000/books/issued/limit/' + this.limit)
            .then(res => res.json())
            .then((data) => {
                var books = data['issued_books']
                for(let i = 0; i < books.length; i++) {
                    let book = books[i]
                    var issuedBook = {}

                    issuedBook['imgSrc'] = book['book_detail']['img_src']
                    
                    let lastTransaction = book['transactions'].slice(-1)[0]
                    let memberId = lastTransaction["member_id"]

                    issuedBook["memberId"] = memberId
                    
                    this.issuedBooks.push(issuedBook)
                }
            })
            .catch(err => console.log(err.message))

        },
    },    
}
</script>

<style>

</style>