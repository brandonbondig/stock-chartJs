<template>
  <div class="d-flex">
    <navbar class="navbar" />
    <sidebar class="sidebar" @changeSecurity="changeSecurity($event)" @changeTimeseries="changeTimeseries($event)"/>
    <div class="d-flex flex-column right">

      <chart :security="security" :key="chart" :timeseries="timeseries"/>
      <infoField class="info" />
    </div>
  </div>
</template>

<script>
import navbar from "./components/navBar.vue";
import sidebar from "./components/sideBar.vue";
import chart from "./components/chartComp.vue";
import infoField from "./components/infoField.vue";

export default {
  name: "App",
  components: {
    navbar,
    sidebar,

    chart,
    infoField,
  },
  data() {
    return {
      security: "SPY",
      timeseries:1000,
      chart: 0
    };
  },
methods:{
    changeSecurity(security)
    {
      this.security=security;
      this.chart += 1
    },
    changeTimeseries(timeseries)
    {
      this.timeseries=timeseries;
      this.chart += 1
    },
}
};
</script>

<style lang="scss">

.right {
  width: 100%;
}
</style>
