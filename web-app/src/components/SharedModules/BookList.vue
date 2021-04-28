<template>
    <div id='book-list-container'>
        <h2 id='book-list-title'> {{this.title}} </h2>
        <li id='book-list' v-for="(value, index) in this.bookList" :key="index">
            <BookCard v-if="index <= this.limit" id='book-card'
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
        limit: {
            type: Number,
            default: 5
        }
    },

}
</script>

<style>
#book-list-container {
    display: flex;
    margin-left: 30px;
    flex-wrap: wrap;
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
    justify-content: flex-start;
}

</style>