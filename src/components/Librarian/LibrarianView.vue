<template>
  <div id="container">
        <Menu id="menu" v-bind:menuContents="this.menuContents" />
        <Home id="home" v-if="acticeScreen === 'Home'" /> 
        <IssueBookPopup 
        v-if="showIssueBookPopup" 
        v-bind:togglePopup="toggleIssueBookPopup"/>  
        <ReturnBookPopup 
            v-if="showReturnBookPopup"
            v-bind:togglePopup="toggleReturnBookPopup"/>
        <MemberPopup
            v-if="showMemberPopup"
            v-bind:togglePopup="toggleMemberPopup"/>
        <ReportsPopup
            v-if="showReportsPopup"
            v-bind:togglePopup="toggleReportsPopup"/>
        <CreateBookPopup
            v-if="showCreateBookPopup"
            v-bind:togglePopup="toggelCreateBookPopup"/>
  </div>
</template>

<script>
import Home from "./Screens/Home"
import Menu from "../SharedModules/Menu"
import IssueBookPopup from "./Moduels/IssueBookPopup"
import ReturnBookPopup from "./Moduels/ReturnBookPopup"
import MemberPopup from "./Moduels/MemberPopup"
import ReportsPopup from "./Moduels/ReportsPopup"
import CreateBookPopup from "./Moduels/CreateBookPopup"


export default {
  name: 'App',
  components: {
    Home,
    Menu,
    IssueBookPopup,
    ReturnBookPopup,
    MemberPopup,
    ReportsPopup,
    CreateBookPopup
  },
  
  data(){
    return {
        menuContents: [
            {
                'title': 'Profile',
                'children':[],
                'clickable': true,
                'onClick': this.showProfileScreen
            },
            {
                'title': 'Books',
                'clickable': false,
                'children':[ 
                    {
                        'title': 'Issue Book',
                        'children': [],
                        'clickable': true,
                        'onClick': this.toggleIssueBookPopup
                    },
                    {
                        'title': 'Return Book',
                        'children': [],
                        'clickable': true,
                        'onClick': this.toggleReturnBookPopup
                    },
                    {
                        'title': 'Manage',
                        'children': [],
                        'clickable': true,
                        'onClick': this.toggelCreateBookPopup
                    },
                ],
            },
            {
                'title': 'Members',
                'children':[],
                'clickable': true,
                'onClick': this.toggleMemberPopup
            },
                        {
                'title': 'Reports',
                'children':[],
                'clickable': true,
                'onClick': this.toggleReportsPopup
            },
            {
                'title': 'Notification',
                'children':[],
                'clickable': true,
                'onClick': this.showNotificationsScreen
            },
            {
                'title': 'Log Out',
                'children':[],
                'clickable': true,
                'onClick': this.showLogoutPopup
            },
        ],
        acticeScreen: "Home",   // Screens : Home, Report, Books, Issued Books, Notifications, Profile, 
        
        showIssueBookPopup: false,
        showReturnBookPopup: false,
        showMemberPopup: false,
        showReportsPopup: false,
        showCreateBookPopup: false,

    }
  },

    methods: {
        // Show screens
        showProfileScreen(){
            console.log("clicked profile")
        },
        toggleMemberPopup(){
            this.showMemberPopup = !this.showMemberPopup
            
        },
        showNotificationsScreen(){
            console.log("clicked notifications")
            
        },
        toggleReportsPopup(){
            this.showReportsPopup = !this.showReportsPopup;

        },

        // Show windows 
        toggleIssueBookPopup(){
            this.showIssueBookPopup = !this.showIssueBookPopup;
            
        },
        toggleReturnBookPopup(){
            this.showReturnBookPopup = !this.showReturnBookPopup;            
        },
        toggelCreateBookPopup(){
            this.showCreateBookPopup = !this.showCreateBookPopup;            
        },

        // Show pop-up
        showLogoutPopup(){
            console.log("clicked logout")

        }
    }
  
}
</script>

<style>
#menu {
  margin: 0;
  padding: 0;
  width: 200px;
  background-color: #F4F5F6;
  position: fixed;
  height: 100%;
  overflow: auto;
}
#home {
  margin:0;
  margin-left: 200px;
  height: 100%;
}
</style>
