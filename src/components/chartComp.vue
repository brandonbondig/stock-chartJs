<template>
  <div class="body">

    <Line v-if="loaded" :chart-data="chartData" :chart-options="chartOptions" :styles="styles" class="chart" />

    <div v-if="!loaded" class="lds-dual-ring"></div>


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
  props: ["security", "timeseries", 'indicator','period'],
  components: { Line },
  data() {
    return {
      chartOptions: {
        interaction: {
          mode: 'index',
          intersect: false,
        },
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
      indicatorPrice: [],
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

    // indicator api
    if (this.indicator != null) {
      const { data } = await axios.get(
        `https://financialmodelingprep.com/api/v3/technical_indicator/daily/${this.security}?period=${this.period}&type=${this.indicator}&apikey=${process.env.VUE_APP_API_KEY}`
      );
      let res = data.slice(0, this.timeseries)

      res.forEach((d) => {
        this.indicatorPrice.push(d[this.indicator])
      })
    }

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
          borderWidth: 3,
        },
        {
          data: this.indicatorPrice.reverse(),
          label:this.indicator,
          borderColor: "#FF0000",
          backgroundColor: '#2D2D2D',
          tension: 0.1,
          pointRadius: 0,
          borderWidth: 3,
        }
      ],
    };
    this.loaded = true;
  },
};
</script>

<style lang="scss" scoped>
.body {
  background-color: #2D2D2D;
  height: 90%;
  width: 100%;
  z-index: 100;
}

.chart {
  background-color: #2D2D2D;
}

.lds-dual-ring {
  display: inline-block;
  width: 80px;
  height: 80px;
  margin-left: 50%;
  margin-top: 15%;

}

.lds-dual-ring:after {
  content: " ";
  display: block;
  width: 64px;
  height: 64px;
  margin: 8px;
  border-radius: 50%;
  border: 6px solid #fff;
  border-color: #fff transparent #fff transparent;
  animation: lds-dual-ring 1.2s linear infinite;
}

@keyframes lds-dual-ring {
  0% {
    transform: rotate(0deg);
  }

  100% {
    transform: rotate(360deg);
  }
}
</style>