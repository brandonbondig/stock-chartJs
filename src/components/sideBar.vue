<template>
  <div class="body">
    <div class="
        form-group
        d-flex
        flex-column
        text-center
        justify-content-center
        form mt-2">
      <p class="">Security</p>
      <input type="text" v-on:keyup.enter="updateChart" placeholder="e.g SPY" class="form-control" v-model="security" />

      <p class="mt-3">Timeseries (days)</p>
      <input type="text" v-on:keyup.enter="updateChart" placeholder="e.g 5" class="form-control" v-model="timeseries" />

      <dropdown @emitTitle="changeIndicator($event)" class="dropdown mt-3" title="Services" :items="indicators"
        :name="'Indicators'" />

      <div class="slidecontainer">
        <p class="mt-3">Indicator Period</p>
        <input type="range" min="1" max="100" class="slider" id="myRange" v-model="sliderVal">
        <br>
        <p class="sliderVal">{{ sliderVal }}</p>

      </div>


      <button class="btn" style="background-color:#BB86FC; font-weight: bold; color: #262626; border-radius: 15px;"
        @click="updateChart">Search</button>



    </div>
  </div>
</template>

<script>
import dropdown from './Dropdown'

export default {
  name: "sidebar",
  components: {
    dropdown
  },
  data() {
    return {
      security: "",
      timeseries: null,
      arrayOfObjects: ['test'],
      newIndicator: null,
      sliderVal: 50,
      object: {
        name: 'Object Name',
      },
      indicators: [
        {
          object: 'SMA',
        },
        {
          object: 'EMA',
        },
        {
          object: 'WMA',
        },
        {
          object: 'DEMA',
        },
        {
          object: 'TEMA',
        },
        {
          object: 'RSI',
        },
        {
          object: 'ADX',
        },
      ],

    };
  },
  methods: {
    updateChart() {
      this.$emit("changeSecurity", this.security.toUpperCase());
      this.$emit("changeTimeseries", this.timeseries);
      this.$emit("period", this.sliderVal);
    },
    changeIndicator(indicator) {
      this.newIndicator = indicator
      this.$emit("changeIndicator", indicator);
    },
    
  },
};
</script>

<style lang="scss" scoped>



.body {
  background-color: #1e1e1e;
  height: 100vh;
  width: 350px;
  z-index: 999;
  box-shadow: 8px 0px 18px 0px rgba(0, 0, 0, 0.35);
}

input {
  width: 75%;
  margin: auto;
  border-radius: 15px;
  background-color: #585858;
  border-color: #1e1e1e;
}


p {
  color: white;
}

button {
  width: 75%;
  margin: auto;
}

.slider {
  -webkit-appearance: none;
  /* Override default CSS styles */
  appearance: none;
  width: 75%;
  /* Full-width */
  height: 25px;
  /* Specified height */
  background: #d3d3d3;
  /* Grey background */
  outline: none;
  /* Remove outline */
  opacity: 0.7;
  /* Set transparency (for mouse-over effects on hover) */
  -webkit-transition: .2s;
  /* 0.2 seconds transition on hover */
  transition: opacity .2s;
}

.sliderVal{
  color: white;
}

</style>