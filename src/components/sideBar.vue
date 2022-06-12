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
        v-on:keyup.enter="onClickButton"
        placeholder="e.g SPY"
        class="form-control"
        v-model="security"
      />
      <p style="cursor: pointer; font-weight: bold">+ Add more</p>
      <button class="btn btn-success" @click="onClickButton">search</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "sidebar",
  data() {
    return {
      security: "",
    };
  },
  methods: {
    onClickButton() {
      this.$emit("changeSecurity", this.security);
    },
  },
};
</script>

<style lang="scss" scoped>
.body {
  background-color: #d9d9d9;
  height: 100vh;
  width: 350px;
  z-index: 999;
  box-shadow: 8px 0px 18px 0px rgba(0,0,0,0.35);
  
}
input {
  width: 75%;
  margin: auto;
  border-radius: 15px;
}

button {
  width: 75%;
  margin: auto;
}
</style>