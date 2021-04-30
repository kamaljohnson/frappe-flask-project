<template>
  <div id="container">
    <LibrarianView v-if="userType==`Librarian`"/>
    <MemberView v-if="userType==`Member`"/>
  </div>
</template>

<script>
import LibrarianView from "./components/Librarian/LibrarianView"
import MemberView from "./components/Member/MemberView"

export default {
  name: 'App',
  components: {
    LibrarianView,
    MemberView,
  },
  data(){
    return {
      userType: "Librarian"  //Member or Librarian  TODO: need to do in a better way
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
