<template>
    <div id="popup">
        <div id="popup-inner">
            <h2 id="title"> Issue Book </h2>
            <div id="member-info-container"> 
                <div id="memer-id-input">
                    <label for="memberId">Member </label>
                    <input v-model="temp_member_id"/>
                    <button 
                        id="get-button"
                        :disabled="temp_member_id === ''" 
                        @click="findMember"> 
                            Find Member 
                    </button> <br/>
                </div>
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
            <div id="book-info-container"> 
                <div id="book-instance-id-input">
                    <label for="bookInstanceId">Book instance </label>
                    <input v-model="temp_book_instance_id"/>
                    <button 
                        id="get-button"
                        :disabled="temp_book_instance_id === ''" 
                        @click="findBookInstance"> 
                            Find Book 
                    </button> <br/>
                </div>
                <div id="book-details"> 
                    <img id="book-pic" :src='bookInstance.pic'>
                    <div id="info-keys">
                        <div> id </div>
                        <div> title </div>
                        <div> author </div>
                        <div> base fees </div>
                        <div> availability </div>
                    </div>
                    <div id="info-values"> 
                        <div> {{bookInstance.id}} </div>
                        <div> {{bookInstance.title}} </div>
                        <div> {{bookInstance.author}} </div>
                        <div> {{bookInstance.baseFees}} </div>
                        <div> {{bookInstance.isAvailable}} </div>
                    </div>
                </div>
            </div>
            <button 
                id="issue-book-button" 
                :disabled="bookInstance.isAvailable === '-' || !bookInstance.isAvailable">
                    Issue Book
                </button>
        </div>
    </div>    
</template>

<script>
export default {
    setup() {
        
    },

    data() {
        return {
            temp_member_id: "",
            temp_book_instance_id: "",

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
        findMember: function() {
            fetch('http://127.0.0.1:5000/members/' + this.temp_member_id)
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
            fetch('http://127.0.0.1:5000/books/instances/' + this.temp_book_instance_id)
            .then(res => res.json())
            .then((data) => {
                var bookInstance = data['book_instance']
                this.bookInstance["id"] = bookInstance['id']
                this.bookInstance["title"] = bookInstance['book_detail']["name"].slice(0, 30)
                this.bookInstance["author"] = bookInstance['book_detail']["author"]
                this.bookInstance["baseFees"] = "₹ " + bookInstance['book_detail']["base_fees"]
                this.bookInstance["pic"] = bookInstance['book_detail']["img_src"]
                this.bookInstance["isAvailable"] = bookInstance["is_available"]
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
    height: 575px;
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


</style>