<template>
  <div id="container">
      <Menu id="menu" v-bind:menuContents="this.menuContents" />
      <Home id="home" v-if="acticeScreen === 'Home'" />   
  </div>
</template>

<script>
import Home from "./Screens/Home"
import Menu from "../SharedModules/Menu"

export default {
  name: 'App',
  components: {
    Home,
    Menu,
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
                        'onClick': this.showIssueBookWindow
                    },
                    {
                        'title': 'Return Book',
                        'children': [],
                        'clickable': true,
                        'onClick': this.showReturnBookWindow
                    },
                    {
                        'title': 'Create New',
                        'children': [],
                        'clickable': true,
                        'onClick': this.showCreateBookWindow
                    },
                ],
            },
            {
                'title': 'Members',
                'children':[],
                'clickable': true,
                'onClick': this.showMembersScreen
            },
                        {
                'title': 'Reports',
                'children':[],
                'clickable': true,
                'onClick': this.showReportScreen
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
    }
  },

    methods: {
        // Show screens
        showProfileScreen(){
            console.log("clicked profile")
        },
        showMembersScreen(){
            console.log("clicked members")
            
        },
        showNotificationsScreen(){
            console.log("clicked notifications")
            
        },
        showReportScreen(){
            console.log("clicked reports")

        },

        // Show windows 
        showIssueBookWindow(){
            console.log("clicked issue book")
            
        },
        showReturnBookWindow(){
            console.log("clicked return book")
            
        },
        showCreateBookWindow(){
            console.log("clicked create book")
        
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
