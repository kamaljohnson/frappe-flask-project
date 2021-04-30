<script>
import { Line } from 'vue3-chart-v2'

export default {
  name: 'LineChart',
  extends: Line,
  props: {
    chartdata: {
      type: Object,
      default: null
    },
    options: {
      type: Object,
      default: null
    }
  },
  mounted () {
    console.log(this.chartdata)
    this.renderChart(this.chartdata, this.options)
  }
}
</script>