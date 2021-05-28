<template>
    <div 
        @click="toggleBookDetailsPopup"
        id='item'>
        <img id='image' :src='this.imgSrc' />
        <table id="info"> 
            <tbody> 
                <tr> 
                    <td>Id</td> <td>: {{this.id}}</td>
                </tr>
                <tr>
                    <td>Name</td> <td>: {{this.bookName}}</td>
                </tr>
                <tr> 
                    <td>Stock </td> <td>: {{this.stock}}</td>
                </tr>
            </tbody>
        </table>
        <CreateBookPopup
            v-if="this.togglePopup"
            v-bind:bookId="this.id"
            v-bind:togglePopup="toggleBookDetailsPopup"/>
    </div>
</template>

<script>
import CreateBookPopup from '../Librarian/Moduels/CreateBookPopup.vue'

export default {
    name: 'BookSearchResultItem',

    props: {
        imgSrc: String,
        id: Number,
        bookName: String,
        stock: Number
    },

    components: {
        CreateBookPopup
    },

    data() {
        return {
            togglePopup: false
        }
    },

    methods: {
        toggleBookDetailsPopup() {
            this.togglePopup = !this.togglePopup
        },
    },

}
</script>

<style>
#item {
    box-shadow:  0px 0px 3px #e1e1e3, 0px 0px 3px #757575;
    padding: 5px;
    border-radius: 10px;
    display: flex;
    flex-direction: row;
    margin-bottom: 10px;
}
#image {
    height: 100px;
    border-radius: 10px;
}
#info {
    display: flex;
    flex-direction: column;
    margin-left: 10px;
}
</style>