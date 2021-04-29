<template>
    <div id="menu-container">
        <div id="blank">
        </div>
        <MenuItem 
            id="menu-items"
            v-for='(menuItem, index) in this.menuContents' 
            :key="index"
            v-bind:menuItem="menuItem"
        />
    </div>
</template>
<script>
import MenuItem from './MenuItem.vue'

export default ({


    props: {
        menuContents: Object,
    },

    components: {
        MenuItem
    },

    setup() {
        
    },

    data() {
        return {

        }
    }
})
</script>


<style>
#blank{
    height: 55px;
}
#menu-items {
    list-style: none;
    text-align: left;
}
</style>