<template>
  <div class="d-flex">
    <navbar class="navbar" @gotoMenu="gotoMenu($emit)" @gotoBook="gotoBook($emit)" :menuActive="menu"
      :bookActive="strategy" :communityActive="community" @gotoCommunity="gotoCommunity($emit)" />

    <sidebar class="sidebar" @changeIndicator="changeIndicator($event)" @changeSecurity="changeSecurity($event)"
      @changeTimeseries="changeTimeseries($event)" @period="getPeriod" />

    <!-- Menu section-->
    <div v-if="menu" class="d-flex flex-column right">
      <infoField class="info" :security="security" :key="chart" />
      <chart :security="security" :key="chart" :timeseries="timeseries" :indicator="indicator" :period="period" />
    </div>

    <!-- Book section -->
    <div v-if="strategy" class="d-flex flex-column right">
      <strategy />
    </div>

    <!-- Community section -->
    <div v-if="community" class="d-flex flex-column right">
      <community />
    </div>

  </div>

</template>


<script>
import navbar from "./components/navBar.vue";
import sidebar from "./components/sideBar.vue";
import chart from "./components/chartComp.vue";
import infoField from "./components/infoField.vue";
import strategy from "./components/sections/strategySection.vue"
import community from './components/sections/communitySection.vue'


export default {
  name: "App",
  components: {
    navbar,
    sidebar,
    strategy,
    community,
    chart,
    infoField,

  },
  // Data
  data() {
    return {
      security: "SPY",
      timeseries: 1000,
      chart: 0,
      menu: true,
      strategy: false,
      community: false,
      indicator: null,
      period: null
    };
  },
  methods: {

    // Change stock ticker and timeseries
    changeSecurity(security) {
      this.security = security;
      this.chart += 1
    },
    changeTimeseries(timeseries) {
      this.timeseries = timeseries;
      this.chart += 1
    },
    // Go to menus ( Main menu, Strategy, Community )
    gotoMenu() {
      this.menu = true
      this.strategy = false
      this.community = false
    },
    gotoBook() {
      this.strategy = true
      this.community = false
      this.menu = false
    },
    gotoCommunity() {
      this.community = true
      this.strategy = false
      this.menu = false

    },
    changeIndicator(indicator) {
      this.indicator = indicator.toLowerCase()
      console.log(indicator);
    },
    getIndicator(indicator) {
      this.choosenIndicator = indicator
      console.log(indicator);
    },
    getPeriod(period) {
      this.period = period
      console.log(period);
    }
  }
};
</script>

<style lang="scss">
@import url('https://fonts.googleapis.com/css2?family=Roboto:ital,wght@0,100;0,300;0,400;0,500;0,700;0,900;1,100;1,300;1,400;1,500;1,700;1,900&display=swap');

#app {
  font-family: 'Roboto', sans-serif;
}

.right {
  width: 100%;
}
</style>
