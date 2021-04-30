<template>
    <div id="popup">
        <div id="popup-inner">
            <h2 id="title"> Issue Book </h2>
            <div id="member-info-container"> 
                <div id="memer-id-input">
                    <label for="memberId">Member </label>
                    <input type="text" id="midInput" name="memberId">
                    <button id="get-button"> Find Member </button> <br/>
                </div>
                <div id="member-details"> 
                    <img id="member-profile-pic" :src='member_profile_pic_src'>
                    <div id="info-keys"> 
                        <div> username </div>
                        <div> email </div>
                        <div> unbilled </div>
                        <div> total paid </div>
                    </div>
                    <div id="info-values"> 
                        <div> kamaljohnson </div>
                        <div> kamaljohnson@gmail.com </div>
                        <div> 100 Rs </div>
                        <div> 150 Rs </div>
                    </div>
                </div>
            </div>
            <div id="book-info-container"> 
                <div id="book-instance-id-input">
                    <label for="bookInstanceId">Book instance </label>
                    <input type="text" id="bidInput" name="bookInstanceId">
                    <button id="get-button"> Find Book </button> <br/>
                </div>
                <div id="book-details"> 
                    <img id="book-pic" :src='book_pic_src'>
                    <div id="info-keys"> 
                        <div> title </div>
                        <div> author </div>
                        <div> base fees </div>
                        <div> stock </div>
                    </div>
                    <div id="info-values"> 
                        <div> Sapiens </div>
                        <div> Yuval Noah Harrari </div>
                        <div> 60 Rs </div>
                        <div> 10 </div>
                    </div>
                </div>
            </div>
            <button id="issue-book-button"> Issue Book</button>
        </div>
    </div>    
</template>

<script>
export default {
    setup() {
        
    },

    data() {
        return {
            member_profile_pic_src: "https://i.pravatar.cc/150",
            book_pic_src: "https://picsum.photos/200/300",
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
}


</style>