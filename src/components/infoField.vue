<template>
  <div class="body shadow-sm p-3 bg-D9D9D9 d-flex">

    <div v-if="loaded" class="companyInfo">
      <div class="first">
        <h1>Asset Name</h1>
        <p>{{ name }}</p>
      </div>

      <div>
        <h1>Asset Price</h1>
        <p>${{ price }} </p>
      </div>

      <div>
        <h1>Asset Change</h1>
        <p>${{ change }}</p>
      </div>

      <div>
        <h1>Percent Change</h1>
        <p>{{ changeP }}%</p>
      </div>

      <div>
        <h1>Exchange</h1>
        <p>{{ exchange }}</p>
      </div>


    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {

  name: "infoField",
  props: ['security'],
  data() {
    return {
      loaded: false,
      changeP: 0,
      change: 0,
      name: '',
      exchange: '',
      price: 0

    }
  },

  async mounted() {

    this.loaded = false;
    //Stock Change
    const data = await axios.get(
      `https://financialmodelingprep.com/api/v3/quote/${this.security}?apikey=${process.env.VUE_APP_API_KEY}`
    );

    this.changeP = parseFloat(data.data[0]['changesPercentage']).toFixed(2)
    this.change = parseFloat(data.data[0]['change']).toFixed(2)
    this.name = data.data[0]['name']
    this.exchange = data.data[0]['exchange']
    this.price = parseFloat(data.data[0]['price']).toFixed(2)

    this.loaded = true;

  },

};
</script>

<style lang="scss" scoped>
.body {
  background-color: #2D2D2D;
  z-index: 998;
  box-shadow: 0px 11px 23px 0px rgba(0, 0, 0, 0.7);
  height: 10%;
  padding: 0%;
}

.companyInfo {
  color: white;
  display: flex;
  font-size: 1.5em;
  position: absolute;

}

h1 {
  font-size: 0.8em;
  font-weight: 200;
  color: #646464;
}

div:not(.body .companyInfo){
  margin-right: 1em;
  text-align: center;
}
</style>