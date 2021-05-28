<template>
    <div id="popup">
        <div id="popup-inner">
            <h2 id="title"> Book </h2>
            <button id="close-window-button" @click="togglePopup()"> X </button>
            <div id="member-info-container"> 
                <div id="memer-id-input">
                    <label for="memberId">Book Detail ID </label>
                    <input v-model="temp_book_detail_id"/>
                    <button 
                        id="get-button"
                        :disabled="temp_book_detail_id === ''" 
                        @click="findBookDetail"> 
                            Find Book 
                    </button>
                    <button 
                    id="get-button"
                    :disabled="temp_book_detail_id !== ''" 
                    @click="newBookDetail"> 
                        New Book 
                    </button>
                </div>
                <div id="member-details"> 
                    <img id="book-pic" :src='book.pic'>
                    <div id="info-keys"> 
                        <div> id </div>
                        <div> title </div>
                        <div> author </div>
                        <div> description </div>
                        <div> base fees </div>
                    </div>
                    <div id="info-values">
                        <div> {{book.id}}</div>
                        <input v-model="book.name"/><div></div>
                        <input v-model="book.author"/><div></div>
                        <input v-model="book.description"/><div></div>
                        <input v-model="book.baseFees"/>
                    </div>
                </div>
            </div>
            <div v-if="create_new">
                <button 
                    id="create-member-button" 
                    @click="createBookDetail">
                        Creat
                </button>
            </div>
            <div 
                id="update-delete-button-container" 
                v-if="exsisting">
                <button
                    id="delete-book-button" 
                    @click="deleteBookDetail">
                        Delete
                </button>
                <button 
                    id="update-book-button" 
                    @click="updateBookDetail">
                        Update
                </button>
                <button 
                    id="add-book-instance-button" 
                    @click="addBookInstance">
                        Add Instance
                </button>
            </div>
        </div>
    </div>    
</template>

<script>

export default {
    props: {
        togglePopup: Function,
        bookId: {
            type: Number,
            default: 0
        },
    },

    mounted() {
        this.temp_book_detail_id = this.bookId
        this.findBookDetail()
    },

    data() {
        return {
            temp_book_detail_id: 0,

            create_new: true,
            exsisting: false,

            book: {
                "id": "-",
                "name": "",
                "author": "",
                "description": "",
                "baseFees": "",
                "pic": "-",
            },
        }
    },

    methods: {
        findBookDetail: function() {
            this.exsisting = true
            this.create_new = false
            fetch('https://blooming-basin-03878.herokuapp.com/books/' + this.temp_book_detail_id)
            .then(res => res.json())
            .then((data) => {
                var book = data['book']
                this.book["id"] = book['id']
                this.book["name"] = book["name"]
                this.book["author"] = book["author"]
                this.book["description"] = book["description"]
                this.book["pic"] = book["img_src"]
                this.book["baseFees"] = "₹ " + book["base_fees"]
            })
            .catch(err => console.log(err.message))
        },
        createBookDetail: function() {
            const requestOptions = {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({
                    name: this.book.name,
                    author: this.book.author,
                    description: this.book.description,
                    base_fees: this.book.baseFees,
                })
            }
            fetch('https://blooming-basin-03878.herokuapp.com/books/create/', requestOptions)
            .then(res => res.json())
            .then((data) => {
                var book = data['book_detail']
                console.log("book : " + book)
                this.$toast.success(`Book ` + book['id'] + ` created successfully`);
                this.togglePopup()

            })
            .catch(err => console.log(err.message))
        },
        updateBookDetail: function() {
            const requestOptions = {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({
                    name: this.book.name,
                    author: this.book.author,
                    description: this.book.description,
                    base_fees: this.book.baseFees.split(' ')[1],
                })
            }
            fetch('https://blooming-basin-03878.herokuapp.com/books/edit/' + this.book.id, requestOptions)
            .then(res => res.json())
            .then((data) => {
                var book = data['book_detail']
                this.$toast.success(`Book  `+ book['id'] + ` updated successfully`);
                this.togglePopup()

            })
            .catch(err => console.log(err.message))
        },
        deleteBookDetail: function() {
            fetch('https://blooming-basin-03878.herokuapp.com/books/delete/' + this.book.id)
            .then(res => res.json())
            .then((data) => {
                var msg = data['msg']
                console.log("msg : " + msg)
                this.$toast.success(`Book  `+ this.book.id + ` deleted successfully`);
                this.togglePopup()

            })
            .catch(err => console.log(err.message))
        },
        addBookInstance: function() { 
            fetch('https://blooming-basin-03878.herokuapp.com/books/add/' + this.book.id)
            .then(res => res.json())
            .then((data) => {
                var book = data['book_instance']
                console.log("book : " + book)
                this.$toast.success(`Book instance `+ book['id'] + ` add successfully`);
                this.togglePopup()
            })
            .catch(err => console.log(err.message))
        },
        newBookDetail: function() {
            this.exsisting = false
            this.create_new = true
            this.book = {
                "id": "-",
                "name": "",
                "author": "",
                "description": "",
                "baseFees": "",
                "pic": "-",
            }
        },
    },
}
</script>

<style scoped>
#popup {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    z-index: 99;
    background-color: rgba(0, 0, 0, 0.2);

    display: flex;
    align-items: center;
    justify-content: center;
    text-align: left;
}

#popup-inner {
    height: 360px;
    width: 600px;
    background: #FFF;
    border-radius: 10px;
    padding: 18px;
}

#member-details {
    margin-top: 10px;
    margin-bottom: 10px;
    height: 208px;
    width: 100%;
    background: rgb(226, 226, 226);
    border-radius: 10px;
    display: flex;
    flex-wrap: wrap;
    font-size: 20px; 
}

#member-profile-pic {
    margin: 20px;
    width: 110px;
    height: 110px;
    border-radius: 20px;
    background: rgb(153, 153, 153);
    padding: 5px;
}

#info-keys {
    margin-top: 30px;
    color: rgb(99, 99, 99);   

}

#info-values {
    margin-top: 30px;
    margin-left: 20px;
    color: rgb(44, 44, 44);   
}

#book-details {
    margin-top: 10px;
    margin-bottom: 10px;
    height: 215px;
    width: 100%;
    background: rgb(226, 226, 226);
    border-radius: 10px;
    display: flex;
    flex-wrap: wrap;
    font-size: 20px; 
}

#book-pic {
    margin: 20px;
    width: 110px;
    height: 165px;
    border-radius: 10px;
    background: rgb(153, 153, 153);
    padding: 5px;
}


#get-button {
    height: 90%;
    margin-left: 10px;
    background: rgb(24, 151, 255);
    border-radius: 4px;
    color: white;
    font-weight: bold;
    border: none;
    padding-left: 10px;
    padding-right: 10px;
    padding-top: 3px;
    padding-bottom: 3px;
    cursor: pointer;
}

#get-button:disabled {
    background: rgb(143, 143, 143);
    cursor: not-allowed;
}

#get-button:hover:enabled {
    background: rgb(1, 124, 224);
}

#create-member-button {
    width: 100%;
    height: 50px;
    font-weight: bold;
    border: none;
    color: white;
    font-size: 25px;
    border-radius: 10px;
    background: rgb(24, 151, 255);
    justify-content: center;
    cursor: pointer;
}

#update-delete-button-container {
    width: 100%;
    height: 50px;
    justify-content: center;
    display: flex;
    flex-wrap: nowrap;
}

#update-book-button {
    width: 33%;
    height: 50px;
    font-weight: bold;
    border: none;
    color: white;
    font-size: 25px;
    border-radius: 10px;
    background: rgb(24, 151, 255);
    justify-content: left;
    cursor: pointer;
    margin-right: 12px;
}

#delete-book-button {
    width: 33%;
    height: 50px;
    font-weight: bold;
    margin-right: 12px;
    border: none;
    color: white;
    font-size: 25px;
    border-radius: 10px;
    background: rgb(255, 59, 24);
    justify-content: right;
    cursor: pointer;
}

#add-book-instance-button {
    width: 33%;
    height: 50px;
    font-weight: bold;
    border: none;
    color: white;
    font-size: 25px;
    border-radius: 10px;
    background: rgb(24, 151, 255);
    justify-content: right;
    cursor: pointer;
}

#create-member-button:disabled {
    background: rgb(143, 143, 143);
    cursor: not-allowed;
}

#create-member-button:hover:enabled {
    background: rgb(1, 124, 224);
}

#close-window-button {
    position: relative;
    float: right;
    background: rgb(253, 65, 65);
	color: white;
    top: -75px;
    border: none;
    right: -5px;
    font-size: 15px;
    border-radius: 5px;
    padding-left: 10px;
    padding-right: 10px;
    padding-top: 5px;
    padding-bottom: 5px;
}

#close-window-button:hover {
    background: rgb(243, 25, 25);
    cursor: pointer;
}

</style>