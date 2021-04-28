<template>
    <div id="insight-container"> 
        <div id="insight-chart-box">
            <table>
                <tbody>
                    <tr v-for='(value, key) in insights' :key=key>
                        <td id="insight-item"> {{key}} </td>
                        <td id="insight-item"> {{value}} </td>
                    </tr>
                </tbody>
            </table>
        </div>
    </div>
</template>
<script>

export default ({

    props: {
        insights: {},
    },

    setup() {
        
    },

    data() {
        return {

        }
    }
})
</script>


<style scoped>
#insight-chart-box {
    margin-top:55px;
    flex-wrap: wrap;
    background: rgb(24, 151, 255);
    padding: 20px;
    border-radius: 10px;
    margin-bottom: 10px;
}
#insight-item {
    text-align: left;
    padding: 8px;
    color: white;
    font-size: 30px;
}

</style>