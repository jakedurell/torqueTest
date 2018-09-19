<template>
<div id="app">
  <div class="containerx">
      <div class="row">
        <LeftPanel class="left-panel col-xs-3"></LeftPanel>
          <div class="col-xs-9 app-body">
              <br>
              <button class="btn btn-primary" @click="selectedComponent = 'Dashboard'">Dashboard</button>
              <button class="btn btn-success" @click="selectedComponent = 'AssetHealth'">Asset Health</button>
              <button class="btn btn-danger"  @click="selectedComponent = 'WorkOrders'">Work Orders</button>
              <hr>
              <Dashboard v-show="selectedComponent === 'Dashboard'" ></Dashboard>
              <AssetHealth v-show="selectedComponent === 'AssetHealth'" :chartObj="chartObj" ></AssetHealth>
              <WorkOrders v-show="(selectedComponent === 'WorkOrders')" ></WorkOrders>
          </div>
      </div>
  </div>
</div>
</template>

<script>
/* eslint-disable */
import LeftPanel from './components/LeftPanel'
import Dashboard from './components/Dashboard'
import AssetHealth from './components/AssetHealth'
import WorkOrders from './components/WorkOrders'
import allData from './assets/data.js'

export default {
  data: function() {
  return {
      quoteTitle: 'The Quote',
      selectedComponent: 'AssetHealth',
      allMotorData: allData,
      oneMotorData: [],
      chartOpenLabel: [],
      chartLastOpenVals: [],
      chartAvgOpenVals: [],
      chartCloseLabel: [],
      chartLastCloseVals: [],
      chartAvgCloseVals: [],
      chartOpenOtherAvg: [],
      chartObj: [],
    }
  },
  name: 'App',
  components: {
    LeftPanel,
    Dashboard,
    AssetHealth,
    WorkOrders
  },
  beforeMount() {
    this.filterMotor('5773df56c8af3c984513abd6');
  },
  methods: {
      filterMotor(motor) {
        this.oneMotorData = this.allMotorData.filter(function(item){
        return item.AssetId === motor; })

        let otherMotorData = [];

        otherMotorData = this.allMotorData.filter(function(item){
        return item.AssetId != motor && item.AssetID !=""; })
        this.prepData(this.oneMotorData, otherMotorData)
      },
      prepData(data, otherMotorData) {
        ///get open data
        let openData = data.filter(function(item){
        return item.Direction === 'Open'; })

        openData.sort(function(a, b){
        return a.Position-b.Position
        })

        let openOtherData = otherMotorData.filter(function(item){
        return item.Direction === 'Open'; })
        // console.log(openOtherData)


        for (let i =0; i < openData.length; i++) {
          this.chartOpenLabel.push(openData[i].Position)
          this.chartLastOpenVals.push(openData[i].LastTorque)
          this.chartAvgOpenVals.push(openData[i].AverageTorque)

          let openOtherDataAtPosition = openOtherData.filter(function(item){
          return item.Position === i; })

          
          let totalOther = 0
          let count = 0

          for (let otherObj of openOtherDataAtPosition) {
            totalOther += otherObj.AverageTorque
            count++
          }

          let totalOtherAvg = totalOther/count
          
          this.chartOpenOtherAvg.push(totalOtherAvg)
          
        }
        console.log(this.chartOpenLabel.length)
        console.log(this.chartOpenOtherAvg)
        ///Get Close Data
        let closeData = data.filter(function(item){
        return item.Direction === 'Open'; })

        closeData.sort(function(a, b){
        return a.Position-b.Position
        })

        for (let i =0; i < openData.length; i++) {
          this.chartCloseLabel.push(closeData[i].Position)
          this.chartLastCloseVals.push(closeData[i].LastTorque)
          this.chartAvgCloseVals.push(closeData[i].AverageTorque)
        }
        
        this.chartObj = [ this.chartOpenLabel, 
                          this.chartLastOpenVals, 
                          this.chartAvgOpenVals,
                          this.chartCloseLabel,
                          this.chartLastCloseVals,
                          this.chartAvgCloseVals]
        }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}



.containerx {
  margin: 20px !important;
}


</style>
