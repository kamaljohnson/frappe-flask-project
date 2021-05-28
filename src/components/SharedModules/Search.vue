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
        <div
            id="search-filters"
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
        <div
            id="search-result"
            v-if="this.search_div_focused || this.search_bar_focused"
        >
            <div
                v-if="this.book_results.length != 0"
            > 
                <h3> Books </h3>
                <div
                    v-if="this.book_results.length != 0"
                > 
                    <li id='book-results' 
                        class="search-result-item"
                        v-for="(value, index) in this.book_results" :key="index"
                    >
                        <books-search-result-item
                            v-bind:imgSrc="value.img_src"
                            v-bind:id="value.id"
                            v-bind:bookName="value.name"
                            v-bind:stock="value.stock"
                        />
                    </li>
                </div>
            </div>
            <div
                v-if="this.member_results.length != 0"
            > 
                <h3> Members </h3>
                <div
                    v-if="this.member_results.length != 0"
                > 
                    <li id='member-results' 
                        class="search-result-item"
                        v-for="(value, index) in this.member_results" :key="index"
                    >
                        <members-search-result-item
                            v-bind:profilePic="value.profile_pic"
                            v-bind:id="value.id"
                            v-bind:username="value.username"
                            v-bind:booksTaken="value.books_taken"
                            v-bind:unbilled="value.unbilled"
                        />
                    </li>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
import BooksSearchResultItem from './BooksSearchResultItem'
import MembersSearchResultItem from './MembersSearchResultItem'

export default {
    name: 'Search',

    components: {
        BooksSearchResultItem,
        MembersSearchResultItem
    },
    
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
            
            book_results: [],
            member_results: []
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
                this.search()
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
            this.search()
        },

        search(){
            this.book_results = this.member_results = []
            if(this.search_word != '') {
                const requestOptions = {
                method: "POST",
                headers: { "Content-Type": "application/json" },
                body: JSON.stringify({
                    search_word: this.search_word,
                    filters: this.filters,
                })
                }
                fetch('https://blooming-basin-03878.herokuapp.com/search', requestOptions)
                .then(res => res.json())
                .then((data) => {
                    console.log("data : " + data['result'])
                    if(data['result']['members'] != null) {
                        console.log('members: ' + data['result']['members'])
                        this.member_results = data['result']['members']
                    }
                    if(data['result']['books'] != null) {
                        console.log('books: ' + data['result']['books'])
                        this.book_results = data['result']['books']
                    }
                })
                .catch(err => console.log(err.message))
            }
        },
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

#search-result {
    margin: 10px;
    margin-top: 40px;
}

.search-result-item {
    list-style: none;
}

</style>