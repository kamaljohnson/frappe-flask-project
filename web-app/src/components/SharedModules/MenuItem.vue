<template>
    <div id="menu-item-container">
        <div 
            id="menu-item-title"
            :style="{
                'margin-left': `${this.depth * 20}px`,
                'font-size': `${18 - ((this.depth -1) * 3)}px`,
            }"
        >
            <h3> {{ this.menuItem.title }} </h3>
        </div>
        <MenuItem 
            id="menu-item" 
            v-for="(subMenuItem, index) in this.menuItem.children" 
            :key="index"
            v-bind:menuItem="subMenuItem"
            v-bind:depth="this.depth + 1"
        />
    </div>
</template>
<script>

export default ({
    
    name: 'MenuItem',

    props: {
        menuItem: Object,
        depth: {
            type: Number,
            default: 1
        }
    },

    mounted() {
        console.log("MENU ITEMS")
        console.log(this.menuItem)
    },

    data() {
        return {

        }
    }
})
</script>


<style>

</style>