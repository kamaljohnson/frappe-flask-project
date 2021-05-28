<template>
    <div
        
        @mouseleave="this.exitFocusSearchDiv()"
        @mouseover="this.focusSearchDiv()"
        tabindex="0"
    >
        <input id="search-input"
            @focus="this.focusSearchBar()"
            @blur="this.exitSearchBar()"
            placeholder="Search"
            v-model="this.search_word"
        />
        <div id="search-body"
            v-if="this.search_div_focused || this.search_bar_focused">
            <button class="filter-button"
                v-bind:style="[
                    this.filters.books ? {
                        background: 'rgb(24, 151, 255)'
                    } : {
                        background: 'rgb(200, 200, 200)'
                    }
                ]"
                @click="this.toggelFilter('books')"
            >
                Books 
            </button>
            <button class="filter-button"
                v-bind:style="[
                    this.filters.members ? {
                        background: 'rgb(24, 151, 255)'
                    } : {
                        background: 'rgb(200, 200, 200)',
                    }
                ]"
                @click="this.toggelFilter('members')"
            > 
                Memebers 
            </button>
        </div>
    </div>
</template>

<script>

export default {
    name: 'Search',
    
    data() {
        return {
            search_word: '',      // topic to be searched,
            filters: {
                'books': true,
                'members': true
            },
            

            user_typing: false,
            typing_flag: false,

            search_div_focused: false,
            search_bar_focused: false,
            
            result: []      // holds search result items
        }
    },

    watch: {
        search_word: function() {
            this.user_typing = true
        },
        user_typing: function(typing) {
            this.typing_flag = true
            if(typing) {
                setTimeout(() => this.user_typing = false, 1000)
                setTimeout(() => this.typing_flag = false, 1500)
            }
        },
        typing_flag: function(flag) {
            if(!flag && !this.user_typing) {
                this.search(this.search_word)
            }
        }
    },

    methods: {
        focusSearchDiv() {
            this.search_div_focused = true
        },
        exitFocusSearchDiv() {
            this.search_div_focused = false
        },
        focusSearchBar(){
            this.search_bar_focused = true
        },
        exitSearchBar(){
            this.search_bar_focused = false
        },
        search(word){
            if(this.search_word != '') {
                console.log("search word: " + word + ' filters: books: ' + this.filters.books + ' members: ' + this.filters.members)
            }
        },

        toggelFilter(filter_name){
            switch(filter_name) {
                case 'books':
                    this.filters.books = !this.filters.books
                    break;
                case 'members': 
                    this.filters.members = !this.filters.members
                    break;
                default:
                    console.log('this code should not be executed')
                    break;
            }
            this.search(this.search_word)
        }
    }

}

</script>

<style>
#search-input{
    border-radius: 10px;
    border: 2px solid #ffffff;
    margin: 2px;
    padding: 5px;
    width: 500px;
    font-size: 20px;
    outline: none;
}

.filter-button {
    border-radius: 10px;
    color: white;
    font-weight: bold;
    border: none;
    margin: 2px;
    padding: 7px;
    padding-left: 12px;
    padding-right: 12px;
    float: right;
}

</style>