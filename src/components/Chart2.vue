//

<script>
/* eslint-disable */
import { Bar } from 'vue-chartjs'
 
export default {
    props: ['chartObj'],
    data: {
        tLabels: [],
        tData: [],
        options: {
            scales: {
                xAxes: [{
                    scaleLabel: {
                        display: true,
                        labelString: 'Valve Position'
                    },
                    ticks: {
                        min: 0,
                        max: 100,
                        stepSize: 10,
                    }
                }],
                yAxes: [{
                    scaleLabel: {
                        display: true,
                        labelString: 'Required torque (%)'
                    },
                    ticks: {
                        autoSkip: true,
                        beginAtZero:true
                    }
                }]
        }
    }
    },
    extends: Bar,
    mounted () {
    // Overwriting base render method with actual data.
        this.renderChart({
        labels: this.chartObj[3],
        datasets: [
            {
            label: 'Average Open Torque',
            backgroundColor: '#236194',
            data: this.chartObj[5],
            },
                        {
            label: 'Last Open Torque',
            backgroundColor: '#90a8ce',
            data: this.chartObj[4],
            }
        ],
        options: this.options
        })
    }
}
</script>

<style scoped>
    div {
        border: 1px solid green;
    }
</style>