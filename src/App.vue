<template scope="{signal}">
<div id="app">
  <div class="container">
      <div class="row">
        <LeftPanel class="left-panel col-xs-3"></LeftPanel>
          <div class="col-xs-9">
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
      chartLabels: [],
      chartVals: [],
      chartObj: []
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
    this.filterMotor('5773d676c8af3c98451361a7');
  },
  methods: {
      filterMotor(motor) {
        this.allMotorData = this.allMotorData.filter(function(item){
        return item.AssetId === motor; })
        this.prepData(this.allMotorData)
      },
      prepData(data) {
        data.sort(function(a, b){
        return a.Position-b.Position
        })

        for (let i =0; i < data.length; i++) {
          this.chartLabels.push(data[i].Position)
          this.chartVals.push(data[i].LastTorque)
        }
        this.chartObj = [this.chartLabels, this.chartVals]
        console.log(this.chartObj)
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

.left-panel {
  width: 25%;
}

</style>
