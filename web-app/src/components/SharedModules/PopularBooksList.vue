<template>
    <div> 
        <h1>Popular Books List</h1>
        <div v-for='book in this.popularBooks' :key=book> 
            <div> img: {{ book['imgSrc'] }} </div> 
            <div v-if='showStock'> stock: {{ book['stock']}} </div>
        </div>
    </div>
</template>

<script>
export default {
    props:{
        showStock: {
            type: Boolean,
            default: true
        }
    },

    data() {
        return {
            popularBooks: []
        }
    },
    
    mounted() {
        this.fetchPopularBooks()
    },

    methods: {
        fetchPopularBooks: function() {
            fetch('http://127.0.0.1:5000/books/popular')
            .then(res => res.json())
            .then((data) => {
                console.log(data)
                var books = data['popular_books']
                for(let i = 0; i < books.length; i++) {
                    let book = books[i]
                    var popularBook = {}
                    popularBook['imgSrc'] = book['img_src']
                    popularBook['stock'] = book['stock']
                    popularBook['popularity'] = book['popularity']
                    this.popularBooks.push(popularBook)
                }
                console.log(this.popularBooks)
            })
            .catch(err => console.log(err.message))
        }
    },    
}
</script>

<style>

</style>