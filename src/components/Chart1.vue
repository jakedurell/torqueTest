//

<script>
import { Bar } from 'vue-chartjs'
 
export default {
    props: ['chartObj'],
    data: {
        tLabels: [],
        tData: []
    },
    extends: Bar,
     beforeMount() {
        this.prepData();
    },
     methods: {
        prepData() {
            console.log(this.chartObj[0])
        }
     },
    mounted () {
    // Overwriting base render method with actual data.
        this.renderChart({
        labels: this.chartObj[0],
        datasets: [
            {
            label: 'Last Torque',
            backgroundColor: 'blue',
            data: this.chartObj[1],
            }
        ]
        })
    }
}
</script>

<style scoped>
    div {
        border: 1px solid green;
    }
</style>