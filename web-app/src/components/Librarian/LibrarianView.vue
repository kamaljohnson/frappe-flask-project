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
                // 'onClick': this.showProfileScreen
            },
            {
                'title': 'Books',
                'children':[ 
                    {
                        'title': 'Issue Book',
                        'children': [],
                        // 'onClick': showIssueBookWindow
                    },
                    {
                        'title': 'Return Book',
                        'children': [],
                        // 'onClick': showReturnBookWindow
                    },
                    {
                        'title': 'Create New',
                        'children': [],
                        // 'onClick': showCreateBookWindow
                    },
                ]
            },
            {
                'title': 'Members',
                'children':[],
                // 'onClick': showMembersScreen
            },
                        {
                'title': 'Reports',
                'children':[],
                // 'onClick': showMembersScreen
            },
            {
                'title': 'Notification',
                'children':[],
                // 'onClick': showNotificationsScreen
            },
            {
                'title': 'Log Out',
                'children':[],
                // 'onClick': showLogoutPopup
            },
        ],
        acticeScreen: "Home",   // Screens : Home, Report, Books, Issued Books, Notifications, Profile, 
    }
  },

    methods: {
        // Show screens
        showProfileScreen(){

        },
        showMembersScreen(){
            
        },
        showNotificationsScreen(){
            
        },
        showReportScreen(){

        },
        showIssuedBooksScreen(){

        },

        // Show windows 
        showIssueBookWindow(){
            
        },
        showReturnBookWindow(){
            
        },
        showCreateBookWindow(){
        
        },

        // Show pop-up
        showLogoutPopup(){

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
