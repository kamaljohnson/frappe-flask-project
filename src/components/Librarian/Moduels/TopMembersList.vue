<template>
    <div id='member-list-container'>
        <h2 id='top-members-title'> {{this.title}} </h2>
        <table id="member-list-table">
            <tbody>
                <tr id='member-slip' v-for="(value, index) in this.topMembersList.slice(0, this.limit)" :key="index" >
                    <td id='member-slip-item'>
                        <img id="profile-pic" :src="value.profilePic"/>
                    </td>
                    <td id='member-slip-item'> {{value.username}} </td>
                    <td id='member-slip-item'>  ₹ {{value.totalPaid + value.unbilled}} </td>
                    <td id='member-slip-item'> {{value.booksTaken}} </td>
                </tr>
            </tbody>
        </table>
    </div>
</template>

<script>

export default {
    name: 'TopMembersList',

    components: {
    },

    data() {
        return {
            title: "Members",
            topMembersList: [],
            limit: 10,
        }
    },
    
    mounted() {
        this.fetchTopMembers()
    },

    methods: {
        fetchTopMembers: function() {
            fetch('https://blooming-basin-03878.herokuapp.com/members/profitable')
            .then(res => res.json())
            .then((data) => {
                var members = data['members']
                for(let i = 0; i < members.length; i++) {
                    let member = members[i]
                    var topMember = {}
                    topMember['username'] = member['username']
                    topMember['profilePic'] = member['profile_pic']
                    topMember['totalPaid'] = member['total_paid']
                    topMember['unbilled'] = member['unbilled']
                    topMember['booksTaken'] = member['books_taken']
                    this.topMembersList.push(topMember)
                }
            })
            .catch(err => console.log(err.message))
        }
    },    
}
</script>

<style>
#top-members-title {
    text-align: start;
    margin-bottom: 10px;
    margin-left: 25px;
}
#member-list-table {
    width: 90%;
    border-spacing: 20px;
    margin-left: 30px;
}

#member-slip {
    box-shadow:  0px 0px 7px #e1e1e3, 0px 0px 7px #757575;
    border-radius:16px;
    background: white;
    text-align: left;
}
#member-slip-item {
    font-size: 25px;
    padding: 5px;
}
#profile-pic {
    height: 60px;
    border-radius:30px;
    padding-top: 8px;
}
</style>