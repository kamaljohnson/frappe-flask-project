<template>
    <div id="report-container"> 
        <h2 id="title">Report</h2>
        <div id="report-chart-box"
            :style="{
                'height': '350px',
                'width': '900px',
                'margin-bottom': '40px'
            }"
        >
            <line-chart
                v-if='loaded'
                v-bind:chartdata='chartData'
                v-bind:options='options'>
            </line-chart>
        </div>
    </div>
</template>

<script>
import LineChart from './LineChart.vue'

export default {
    name: 'ReportChart',
    
    components: { 
        LineChart
    },

    data() {
        return {
            loaded: false,
            chartData: null,
            reports: [],
            options: null,
        }
    },

    mounted() {
        this.fetchReports()
    },

    methods: {
        fetchReports: function() {
            this.loaded = false
            fetch('http://127.0.0.1:5000/library/reports/all/30')
            .then(res => res.json())
            .then((data) => {
                console.log(data)
                this.reports = data['reports']
                this.getChartDataFromReports()
            })
            .catch(err => console.log(err.message))
        },

        getChartDataFromReports: function() {
            let earnings = []
            let books_issued = []
            
            let day_labels = []

            for (let index = this.reports.length - 1; index >= 0 ; index--) {
                const report = this.reports[index];
                earnings.push(report.earnings)
                books_issued.push(report.books_issued)
                let day_label = report.date.slice(4, 12)
                day_labels.push(day_label)
            }    

            this.chartData = {
                labels: day_labels,
                datasets: [
                    {
                        label: 'Earnings',
                        data: earnings,
                        yAxisID: 'earnings',
                        borderWidth: 3,
                        borderColor: '#3F91F2',
                        fill: false,
                        tension: 0.1

                    },
                    {
                        label: 'Books Issued',
                        data: books_issued,
                        yAxisID: 'books_issued',
                        borderWidth: 3,
                        borderColor: '#727272',
                        fill: false,
                        tension: 0.1
                    }
                ]
            }

            this.options = {
                responsive: true,
                maintainAspectRatio: false,
                scales: {
                    yAxes: [
                        {
                            id: 'earnings',
                            position: 'left',
                            gridLines: {
                                display: false
                            },
                            ticks: {
                                    beginAtZero: true
                            }
                        }, 
                        {
                            id: 'books_issued',
                            position: 'right',
                            gridLines: {
                                display: false
                            },
                            ticks: {
                                    beginAtZero: true
                            }
                        }
                    ],
                    xAxes: [
                        {
                            gridLines: {
                                display: false
                            }
                        }, 
                    ],
                },
            }
            
            this.loaded = true
        }
    },
}
</script>

<style scoped>
#title {
    text-align: start;
    margin-bottom: 10px;
}
</style>