//

<script>
import { Bar } from 'vue-chartjs'
 
export default {
    props: ['chartData'],
    data: {
        tLabels: [],
        tData: []
    },
    extends: Bar,
     beforeMount() {
        this.prepData(this.$props.chartData);
    },
     methods: {
        prepData(data) {
            data.sort(function(a, b){
            return a.Position-b.Position
            })
            console.log(data)
        }
     },
    mounted () {
    // Overwriting base render method with actual data.
        this.renderChart({
        labels: ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December'],
        datasets: [
            {
            label: 'GitHub Commits',
            backgroundColor: 'blue',
            data: [40, 20, 12, 39, 10, 40, 39, 80, 40, 20, 12, 11]
            },
            {
            label: 'Yup',
            backgroundColor: 'red',
            data: [40, 20, 12, 39, 10, 40, 39, 80, 40, 20, 12, 11]
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