<template>
    <div id='item'>
        <img id='image' :src='this.profilePic' />
        <table id="info"> 
            <tbody> 
                <tr> 
                    <td>Id</td> <td>: {{this.id}}</td>
                </tr>
                <tr>
                    <td>Name</td> <td>: {{this.username}}</td>
                </tr>
                <tr> 
                    <td>Books Taken </td> <td>: {{this.booksTaken}}</td>
                </tr>
                <tr> 
                    <td>Unbilled </td> <td>: {{this.unbilled}}</td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>
export default {
    name: 'BookSearchResultItem',

    props: {
        profilePic: String,
        id: Number,
        username: String,
        unbilled: Number,
        booksTaken: Number,
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