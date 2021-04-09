<template>
    <div>
        <div id="top-container">
            <h1 id='hi-username'>Hi {{username}} 😊</h1>
            <Search id='search-box'/>
        </div>
        <div id="report-insight-container">
            <ReportChart id='report-view'/>
            <Insight id='insight'/>
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
            username: 'Kamal'
        }
    },
}
</script>

<style> 
#top-container{
    margin-top: 0px;
    padding: 10px;
}
#hi-username {
    float: left;
    padding-left: 30px;
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