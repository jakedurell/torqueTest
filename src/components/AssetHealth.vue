<template>
    <div>
        <slot name="assetHealth">
            <Chart1 :chartData="chartData"></Chart1>
        </slot>
    </div>
</template>

<script>
import Chart1 from './Chart1'

export default {
props: ['chartData'],
  components: {
    Chart1,
  }
}

</script>

<style scoped>
    div {
        border: 1px solid green;
        background-color: lightgreen;
        padding: 30px;
        margin: 20px auto;
        text-align: center
    }
</style>