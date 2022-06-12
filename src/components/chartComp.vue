<template>
  <div class="body">
    <Line
      v-if="loaded"
      :chart-data="chartData"
      :chart-options="chartOptions"
      :styles="styles"
     class="chart"/>
  </div>
</template>

<script>
import axios from "axios";
import { Line } from "vue-chartjs";

import {
  Chart as ChartJS,
  Title,
  Tooltip,
  Legend,
  LineElement,
  LinearScale,
  PointElement,
  CategoryScale,
  Filler
} from "chart.js";
ChartJS.register(
  Title,
  Tooltip,
  Legend,
  LineElement,
  LinearScale,
  PointElement,
  CategoryScale,
  Filler
);

export default {
  name: "chart",
  props: ["security", "timeseries"],
  components: { Line },
  data() {
    return {
      chartOptions: {
        scales: {
          //hides the y axis
          y: {
            grid: {
              color: "#383838",
              borderColor: '#2D2D2D',
            },
          },
          x: {
            grid: {
              display: false,
              borderColor: '#383838',
            },
          },
          
        },
        maintainAspectRatio: false,
      },
      label: [],
      price: [],
      loaded: false,
      chartData: null,
    };
  },
  computed: {
    styles() {
      return {
        height: "100%",
        width: "100%",
      };
    },
  },

  async mounted() {
    this.loaded = false;

    //stock api
    const stock = await axios.get(
      `https://financialmodelingprep.com/api/v3/historical-price-full/${this.security}?timeseries=${this.timeseries}&apikey=${process.env.VUE_APP_API_KEY}`
    );

    stock.data.historical.forEach((d) => {
      this.price.push(d.close);
      this.label.push(d.date);
    });
    
    this.chartData = {
      labels: this.label.reverse(),
      datasets: [
        {
          backgroundColor: '#2D2D2D',
          label: this.security,
          data: this.price.reverse(),
          borderColor: "#BB86FC",
          backgroundColor: '#2D2D2D',
          tension: 0.1,
          pointRadius: 0,
          borderWidth: 2,
        },
      ],
    };
    this.loaded = true;
  },
};
</script>

<style lang="scss" scoped>
.body {
  background-color: #ffffff;
  height: 60%;
  width: 100%;
}

.chart{
  background-color: #2D2D2D;
}
</style>