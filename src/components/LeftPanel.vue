<template>
  <div class="leftDiv">
    <h1 id="overview">Terminal Overview</h1>
    <img src=".././assets/terminal.jpg">
    <h1>Terminal Name</h1>
    <p>{{ terminalName }}</p>
    <h1>Country Code</h1>
    <p>{{ CountryCode }}</p>
    <h1>Address</h1>
  </div>
</template>

<script>
export default {
  name: 'LeftPanel',
  data () {
    return {
      terminalName: 'WEST',
      CountryCode: 'NLD'
    }
  }
}
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style scoped>
#overview {
  background-color: blue;
  color: white;
}
h1, h2 {
  font-weight: bold;
  font-size: 25px;
}
p {
  font-size: 20px;
}
.leftDiv {
  text-align: left;
  border:solid 1px grey;
}
 img {
   max-width: 100%;
 }
</style>
