<template>
    <div id='book-card'>
        <img id='book-image' :src='this.imgSrc' />
        <div 
            id='book-stock' 
            v-if="this.stock != -1">
            {{this.stock}} 
        </div>
        <div 
            id='member-icon' 
            v-if="this.memberId != ''">
            <img id="member-icon-img" :src="this.memberProfilePic"/>
        </div>
        
    </div>
</template>

<script>
export default {
    name: 'BookCard',

    props: {
        imgSrc: String,
        memberId: {
            type: String,
            default: ''
        },
        stock: {
            type: Number,
            default: -1
        },
    },

    data() {
        return {
            memberProfilePic: ""
        }
    },

    mounted() {
        if(this.memberId != "") {
            this.fetchMember()
        }
    },

    methods: {
        fetchMember: function() {
            fetch('https://blooming-basin-03878.herokuapp.com/members/' + this.memberId)
            .then(res => res.json())
            .then((data) => {
                var member = data['member']
                this.memberProfilePic = member['profile_pic']
            })
            .catch(err => console.log(err.message))
        }
    },

}
</script>

<style>
#book-card {
    position: relative;
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
    position:absolute;
    bottom: 10px;
    right: 6px;
    width: 27px;
    background: rgb(24, 151, 255);
    color: rgb(255, 255, 255);
    font-weight:bolder;
    font-size: 25px;
    padding: 10px;
    border-radius: 25px;
}

#member-icon-img {
    position:absolute;
    bottom: 10px;
    right: 6px;
    height: 70px;
    border-radius: 35px;
    background: rgb(255, 255, 255);
    padding: 4px;
}
</style>