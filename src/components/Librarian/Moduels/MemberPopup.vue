<template>
    <div id="popup">
        <div id="popup-inner">
            <h2 id="title"> Member </h2>
            <button id="close-window-button" @click="togglePopup()"> X </button>
            <div id="member-info-container"> 
                <div id="memer-id-input">
                    <label for="memberId">Member </label>
                    <input v-model="temp_member_id"/>
                    <button 
                        id="get-button"
                        :disabled="temp_member_id === ''" 
                        @click="findMember"> 
                            Find Member 
                    </button>
                    <button 
                    id="get-button"
                    :disabled="temp_member_id !== ''" 
                    @click="newMember"> 
                        New Member 
                    </button>
                </div>
                <div id="member-details"> 
                    <img id="member-profile-pic" :src='member.profilePic'>
                    <div id="info-keys"> 
                        <div> id </div>
                        <div> username </div>
                        <div> email </div>
                    </div>
                    <div id="info-values">
                        <div> {{member.id}}</div>
                        <input v-model="member.username"/>
                        <div></div>
                        <input v-model="member.email"/>
                    </div>
                </div>
            </div>
            <div v-if="create_new">
                <button 
                    id="create-member-button" 
                    @click="createMember">
                        Create
                </button>
            </div>
            <div 
                id="update-delete-button-container" 
                v-if="exsisting">
                <button
                    id="delete-member-button" 
                    @click="deleteMember">
                        Delete
                </button>
                <button 
                    id="update-member-button" 
                    @click="updateMember">
                        Update
                </button>
            </div>
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
            temp_member_id: "",

            create_new: true,
            exsisting: false,

            member: {
                "id": "-",
                "username": "",
                "email": "",
                "profilePic": "-",
            },
        }
    },

    methods: {
        findMember: function() {
            this.exsisting = true
            this.create_new = false
            fetch('https://blooming-basin-03878.herokuapp.com/members/' + this.temp_member_id)
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
        createMember: function() {
            const requestOptions = {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({
                    username: this.member.username,
                    email: this.member.email,
                })
            }
            fetch('https://blooming-basin-03878.herokuapp.com/members/create', requestOptions)
            .then(res => res.json())
            .then((data) => {
                var member = data['member']
                console.log("member : " + member)
                this.$toast.success(`Member ` + member['id'] + ` created successfully`);
                this.togglePopup()

            })
            .catch(err => console.log(err.message))
        },
        updateMember: function() {
            const requestOptions = {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({
                    username: this.member.username,
                    email: this.member.email,
                })
            }
            fetch('https://blooming-basin-03878.herokuapp.com/members/edit/' + this.member.id, requestOptions)
            .then(res => res.json())
            .then((data) => {
                var member = data['member']
                console.log("member : " + member)
                this.$toast.success(`Member  `+ member['id'] + ` updated successfully`);
                this.togglePopup()

            })
            .catch(err => console.log(err.message))
        },
        deleteMember: function() {
            fetch('https://blooming-basin-03878.herokuapp.com/members/delete/' + this.member.id)
            .then(res => res.json())
            .then((data) => {
                var msg = data['msg']
                console.log("msg : " + msg)
                this.$toast.success(`Member  `+ this.member.id + ` deleted successfully`);
                this.togglePopup()

            })
            .catch(err => console.log(err.message))
        },
        newMember: function() {
            this.exsisting = false
            this.create_new = true
            this.member.id = '-'
            this.member.username = ''
            this.member.email = ''
            this.member.profilePic = ''
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
    height: 310px;
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

#update-member-button {
    width: 50%;
    height: 50px;
    font-weight: bold;
    border: none;
    color: white;
    font-size: 25px;
    border-radius: 10px;
    background: rgb(24, 151, 255);
    justify-content: left;
    cursor: pointer;
}

#delete-member-button {
    width: 50%;
    height: 50px;
    margin-right: 12px;
    font-weight: bold;
    border: none;
    color: white;
    font-size: 25px;
    border-radius: 10px;
    background: rgb(255, 59, 24);
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