<template>
    <div id='book-card'>
        <img id='book-image' :src='this.imgSrc' />
        <div id='book-stock'> STOCK {{this.stock}} </div>
    </div>
</template>

<script>
export default {
    name: 'BookCard',

    props: {
        imgSrc: String,
        stock: Number,
    }

}
</script>

<style>
#book-card {
    box-shadow:  0px 0px 7px #e1e1e3, 0px 0px 7px #757575;
    border-radius:16px;
    background: white;
    margin-left: 15px;
    margin-right: 5px;
    margin-top: 25px;
    margin-bottom: 25px;
}
#book-image {
    width: 150px;
    padding: 3px;
    border-radius:16px;
}
#book-stock {
    padding: 0px;
    margin: 0px;
}
</style>