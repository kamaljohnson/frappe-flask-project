<template>
    <div id='book-list-container'>
        <h2 id='book-list-title'> {{this.title}} </h2>
        <li id='book-list' v-for="(value, index) in this.bookList" :key="index">
            <BookCard v-if="index < this.limit" id='book-card'
                v-bind:imgSrc='value.imgSrc'
                v-bind:stock='value.stock'>
            </BookCard>
            <div id="end-card-container" v-if="index === this.limit">
                <button id="load-more-button"> 
                    More
                </button>
            </div>
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
            default: 7
        }
    },

}
</script>

<style>
#book-list-container {
    display: flex;
    margin-left: 30px;
    flex-wrap: wrap;
    justify-content: flex-start;
}
#book-list-title {
    text-align: start;
    width: 100%;
    margin-bottom: 10px;
}
#book-list {
    list-style: none;
    background: rgb(244, 245, 246);
}
#end-card-container {
    height: 100%;
}
#load-more-button {
    background: gray;
    text-align: center;
    padding: 8px;
    margin-left: 10px;
    color: white;
    height: 100%;
    width: 100%;
    font-size: 20px;
}

</style>