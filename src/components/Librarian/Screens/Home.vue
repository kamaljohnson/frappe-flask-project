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
                'Total Books': 0,
                'Books Issued': 0,
                'Members': 0,
                'Total Earnings': 0
            },
        }
    },

    mounted() {
        this.fetchInsights()
    },

    methods: {
        fetchInsights: function() {
            fetch('https://blooming-basin-03878.herokuapp.com/library/insight')
            .then(res => res.json())
            .then((data) => {
                console.log(data)
                this.insight['Total Books'] = data['insight']['total_books']
                this.insight['Books Issued'] = data['insight']['books_issued']
                this.insight['Members'] = data['insight']['members']
                this.insight['Total Earnings'] = data['insight']['total_earnings']
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
    z-index: 98;
    max-width: 600px;
    position: absolute;
    right: 0px;
    border: 2px solid #868686;
    border-radius: 20px;
    text-align: start;
    margin-right: 20px;
    margin-top: 0;
    padding: 5px;
    background: white;
}
</style>