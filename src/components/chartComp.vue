<template>
  <div class="body">
    {{ security }}
  </div>
</template>

<script>
export default {
  name: "chart",
  props: ["security"],
};
</script>

<style lang="scss" scoped>
.body {
  background-color: #ffffff;
  height: 60%;
  width: 100%;
}
</style>