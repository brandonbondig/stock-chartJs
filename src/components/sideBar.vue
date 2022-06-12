<template>
  <div class="body">
    <div
      class="
        form-group
        d-flex
        flex-column
        text-center
        justify-content-center
        form
        mt-3
      "
    >
      <p class="">Security</p>
      <input
        type="text"
        style="text-transform: uppercase"
        v-on:keyup.enter="updateChart"
        placeholder="e.g SPY"
        class="form-control"
        v-model="security"
      />
      <p class="mt-3">Timeseries (days)</p>
      <input
        type="text"
        v-on:keyup.enter="updateChart"
        placeholder="e.g 5"
        class="form-control mb-3"
        v-model="timeseries"
      />
      <button class="btn" style="background-color:#BB86FC; font-weight: bold; color: #262626; border-radius: 15px;" @click="updateChart">Search</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "sidebar",
  data() {
    return {
      security: "",
      timeseries: null,
    };
  },
  methods: {
    updateChart() {
      this.$emit("changeSecurity", this.security);
      this.$emit("changeTimeseries", this.timeseries);
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



p{
  color: white;
}

button {
  width: 75%;
  margin: auto;
}
</style>