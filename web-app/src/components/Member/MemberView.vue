<template>
  <div id="container">
      <Menu id="menu"/>
      <Home />
  </div>
</template>

<script>
import Home from "./Home"
import Menu from "../SharedModules/Menu"

export default {
  name: 'App',
  components: {
    Home,
    Menu,
  },
  data(){
    return {
    
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
