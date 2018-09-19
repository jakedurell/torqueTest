<template>
    <div>
        <slot name="assetHealth">
            <Chart1 :chartObj="chartObj"></Chart1>
        </slot>
    </div>
</template>

<script>
import Chart1 from './Chart1'

export default {
props: ['chartObj'],
beforeMount() {
        console.log(this.chartObj);
},
components: {
    Chart1,
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
</style>