<template>
    <div id="popup">
        <div id="popup-inner">
            <h2 id="title"> Return Book </h2>
            <button id="close-window-button" @click="togglePopup()"> X </button>
            <div id="book-info-container"> 
                <div id="book-instance-id-input">
                    <label for="bookInstanceId">Book instance </label>
                    <input v-model="temp_book_instance_id"/>
                    <button 
                        id="get-button"
                        :disabled="temp_book_instance_id === ''" 
                        @click="findBookInstance"> 
                            Find 
                    </button> <br/>
                </div>
                <div id="book-details"> 
                    <img id="book-pic" :src='bookInstance.pic'>
                    <div id="info-keys">
                        <div> id </div>
                        <div> title </div>
                        <div> author </div>
                        <div> base fees </div>
                    </div>
                    <div id="info-values"> 
                        <div> {{bookInstance.id}} </div>
                        <div> {{bookInstance.title}} </div>
                        <div> {{bookInstance.author}} </div>
                        <div> {{bookInstance.baseFees}} </div>
                    </div>
                </div>
            </div>
            <div id="member-info-container"> 
                <div id="member-details"> 
                    <img id="member-profile-pic" :src='member.profilePic'>
                    <div id="info-keys"> 
                        <div> id </div>
                        <div> username </div>
                        <div> email </div>
                        <div> unbilled </div>
                    </div>
                    <div id="info-values">
                        <div> {{member.id}} </div>
                        <div> {{member.username}} </div>
                        <div> {{member.email}} </div>
                        <div> {{member.unbilled}} </div>
                    </div>
                </div>
            </div>
                <div id="bill-info-container"> 
                <div id="bill-details"> 
                    <div id="bill-info-keys"> 
                        <div> transaction id </div>
                        <div> issue date </div>
                        <div> total fees </div>
                    </div>
                    <div id="bill-info-values">
                        <div> {{transaction.id}} </div>
                        <div> {{transaction.issueDate}} </div>
                        <div> {{transaction.fees}} </div>
                    </div>
                </div>
            </div>
            <button 
                id="issue-book-button" 
                :disabled="bookInstance.isAvailable"
                @click="returnBook">
                    Return Book
                </button>
        </div>
    </div>    
</template>

<script>

export default {
    setup() {
    },

    props: {
        togglePopup: Function
    },

    data() {
        return {
            temp_book_instance_id: "",
            transaction: {
                "id": "-",
                "issueDate": "-",
                "fees": "-"
            },

            member: {
                "id": "-",
                "username": "-",
                "email": "-",
                "unbilled": "-",
                "profilePic": "-",
            },
            bookInstance: {
                "id": "-",
                "title": "-",
                "author": "-",
                "baseFees": "-",
                "pic": "-",
                "isAvailable": "-",
            },
        }
    },

    methods: {
        getMember: function() {
            fetch('https://blooming-basin-03878.herokuapp.com/members/' + this.member.id)
            .then(res => res.json())
            .then((data) => {
                var member = data['member']
                this.member["id"] = member['id']
                this.member["username"] = member["username"]
                this.member["email"] = member["email"]
                this.member["unbilled"] = "₹ " + member["unbilled"]
                this.member["profilePic"] = member["profile_pic"]
            })
            .catch(err => console.log(err.message))
        },
        findBookInstance: function() {
            fetch('https://blooming-basin-03878.herokuapp.com/books/instances/' + this.temp_book_instance_id)
            .then(res => res.json())
            .then((data) => {
                var bookInstance = data['book_instance']

                if(bookInstance["is_available"]) {
                    this.$toast.error(`Book not yet issued !`);
                    return
                }

                this.bookInstance["id"] = bookInstance['id']
                this.bookInstance["title"] = bookInstance['book_detail']["name"].slice(0, 30)
                this.bookInstance["author"] = bookInstance['book_detail']["author"]
                this.bookInstance["baseFees"] = "₹ " + bookInstance['book_detail']["base_fees"]
                this.bookInstance["pic"] = bookInstance['book_detail']["img_src"]
                this.bookInstance["isAvailable"] = bookInstance["is_available"],
                this.bookInstance["transactions"] = bookInstance["transactions"]

                for(var index = 0; index < this.bookInstance.transactions.length; index++) {
                    const transaction = this.bookInstance.transactions[index] 
                    if(!transaction["returned"]) {
                        this.member.id   = transaction["member_id"]
                        
                        this.transaction.id = transaction['id'],
                        this.transaction.issueDate = transaction['issue_date'].slice(0, 16)
                        this.transaction.fees = transaction['fees']
                        
                        this.getMember()
                    }
                }
            })
            .catch(err => console.log(err.message))
        },
        returnBook: function() {
            console.log("returning book")
            fetch('https://blooming-basin-03878.herokuapp.com/transactions/return_book/' + this.bookInstance.id)
            .then(res => res.json())
            .then((data) => {
                var transaction = data['transaction']
                var returned = transaction['returned']
                if(returned) {
                    this.$toast.success(`Book returned successfully`);
                    this.togglePopup()
                }

            })
            .catch(err => console.log(err.message))
        }
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
    height: 645px;
    width: 600px;
    background: #FFF;
    border-radius: 10px;
    padding: 18px;
}

#member-details {
    margin-top: 10px;
    margin-bottom: 10px;
    height: 158px;
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

#bill-details {
    margin-bottom: 10px;
    height: 100px;
    width: 100%;
    background: rgb(226, 226, 226);
    border-radius: 10px;
    display: flex;
    flex-wrap: wrap;
    font-size: 20px;
}

#bill-info-keys {
    margin-left: 20px;
    margin-top: 15px;
    color: rgb(99, 99, 99);   

}

#bill-info-values {
    margin-top: 15px;
    margin-left: 20px;
    color: rgb(44, 44, 44);   
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

#issue-book-button {
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

#issue-book-button:disabled {
    background: rgb(143, 143, 143);
    cursor: not-allowed;
}

#issue-book-button:hover:enabled {
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