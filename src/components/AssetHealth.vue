<template>
    <div>
        <slot name="assetHealth">
            <h1>OPEN</h1>
            <Chart1 :chartObj="chartObj" class="chart"></Chart1>
            <h1>CLOSE</h1>
            <Chart2 :chartObj="chartObj" class="chart"></Chart2>
        </slot>
    </div>
</template>

<script>
/* eslint-disable */
import Chart1 from './Chart1'
import Chart2 from './Chart2'

export default {
props: ['chartObj'],
beforeMount() {
        // console.log(this.chartObj);
},
components: {
    Chart1,
    Chart2
  }
}

</script>

<style scoped>
    div {
        border: 1px solid green;
        padding: 30px;
        margin: 20px auto;
        text-align: center
    }
    h1 {
        text-align: left;
    }
    .chart {
        width: 100%;
    }
</style>