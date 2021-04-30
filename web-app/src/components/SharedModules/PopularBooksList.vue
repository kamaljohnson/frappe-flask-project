<template>
    <div> 
        <BookList 
            v-bind:title='this.title'
            v-bind:bookList='this.popularBooks'
            v-bind:limit='7'>
        </BookList> 
    </div>
</template>

<script>
import BookList from '../SharedModules/BookList'

export default {
    name: 'PopularBooksList',

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
            title: "Popular Books",
            popularBooks: []
        }
    },
    
    mounted() {
        this.fetchPopularBooks()
    },

    methods: {
        fetchPopularBooks: function() {
            fetch('https://blooming-basin-03878.herokuapp.com/books/popular')
            .then(res => res.json())
            .then((data) => {
                var books = data['popular_books']
                for(let i = 0; i < books.length; i++) {
                    let book = books[i]
                    var popularBook = {}
                    popularBook['imgSrc'] = book['img_src']
                    popularBook['stock'] = book['stock']
                    popularBook['popularity'] = book['popularity']
                    this.popularBooks.push(popularBook)
                }
            })
            .catch(err => console.log(err.message))
        }
    },    
}
</script>

<style>

</style>