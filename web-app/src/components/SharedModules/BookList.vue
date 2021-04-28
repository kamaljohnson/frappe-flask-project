<template>
    <div id='book-list-container'>
        <h2 id='book-list-title'> {{this.title}} </h2>
        <li id='book-list' v-for="(value, index) in this.bookList" :key="index">
            <BookCard id='book-card'
                v-bind:imgSrc='value.imgSrc'
                v-bind:stock='value.stock'>
            </BookCard>
        </li>
    </div>
</template>

<script>
import BookCard from './BookCard'

export default {
    name: 'BookList',

    components: {
        BookCard
    },

    props: {
        title:String,
        bookList:Array,
    }

}
</script>

<style>
#book-list-container {
    flex-wrap: wrap;
    display: flex;
    align-content: left;
    margin-left: 30px;
}
#book-list-title {
    text-align: start;
    width: 100%;
    margin-bottom: 10px;
}
#book-list {
    background: lightgray;
    list-style: none;
    padding: 10px;
    display: inline-block;
}

</style>