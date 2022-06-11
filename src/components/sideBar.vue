<template>
  <div class="body">
    <div class="form-group d-flex flex-column text-center justify-content-center form">
      <p class="m-0">Security</p>
      <input type="text" placeholder="e.g SPY" class="form-control" v-model="security">
      <p style="cursor:pointer; font-weight:bold;">+ Add more</p>
      <button class="btn btn-success" @click="onClickButton">search</button>
    </div>
  </div>
</template>

<script>
export default {
  name: "sidebar",
  data(){
    return{
      security:""
    }
  },
  methods:{
    onClickButton() {
    this.$emit('changeSecurity', this.security)
    }
  }
};
</script>

<style lang="scss" scoped>
.body {
  background-color: #D9D9D9;
  height: 100vh;
  width: 350px;
}
input{
  width: 75%;
  margin: auto;
}

button{
  width: 75%;
  margin: auto;
}
</style>