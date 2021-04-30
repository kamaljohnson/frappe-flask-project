<template>
    <div>
        <div id="top-container">
            <h1 id='hi-username'>Hi {{username}} 😊</h1>
            <Search id='search-box'/>
        </div>
        <div id="report-insight-container">
            <ReportChart id='report-chart'/>
            <Insight id='insight' v-bind:insights='insight'/>
        </div>
        <PopularBooksList id='popular-books-list'/>
        <IssuedBooksList id='issued-books-list'/>
        <TopMembersList id='top-members-view'/>
    </div>
</template>

<script>
import Search from '../../SharedModules/Search'
import ReportChart from '../Moduels/ReportChart'
import TopMembersList from '../Moduels/TopMembersList'
import IssuedBooksList from '../Moduels/IssuedBooksList'
import Insight from '../../SharedModules/Insight'
import PopularBooksList from '../../SharedModules/PopularBooksList'

export default {
    name: 'Home',

    components: {
        Search,
        ReportChart,
        TopMembersList,
        IssuedBooksList,
        Insight,
        PopularBooksList
    },

    data(){
        return {
            username: 'Kamal',
            insight: {
                'total_books': 0,
                'books_issued': 0,
                'members': 0,
                'total_earnings': 0
            },
        }
    },

    mounted() {
        this.fetchInsights()
    },

    methods: {
        fetchInsights: function() {
            fetch('http://127.0.0.1:5000/library/insight')
            .then(res => res.json())
            .then((data) => {
                console.log(data)
                this.insight = data['insight']
            })
            .catch(err => console.log(err.message))
        }
    }
}
</script>

<style scoped> 
#report-insight-container {
    margin-left: 30px;
    margin-top: 55px;
    width: 100%;
    display: flex;
    flex-wrap: wrap;
    flex-direction: row;
    justify-content: flex-start;
    align-content: flex-start;
}
#report-chart {
    margin-right: 20px;
}
#insight {
    margin-right: 30px;
}
#top-container{
    margin-top: 0px;
    padding: 10px;
}
#hi-username {
    float: left;
    padding-left: 20px;
    margin-top: 0px;
}
#search-box {
    float: right;
    width: 500px;
    background: #F4F5F6;
    text-align: start;
    margin-right: 20px;
    margin-top: 0;
    padding: 10px;
}
</style>