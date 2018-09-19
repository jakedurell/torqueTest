<template>
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
                <keep-alive>
                    <component :is="selectedComponent">
                        <p slot="Dashboard">I am a blue box!</p>
                        <p :chartData="allMotorData"  slot="AssetHealth">I am a green box!</p>
                        <p slot="WorkOrders">I am a red box!</p>
                    </component>
                </keep-alive>
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
                allMotorData:  allData,
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
