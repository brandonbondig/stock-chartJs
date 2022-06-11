<template>
<div class="body border-right">
  <div class="navGroup">
    <img src="../assets/menu.svg" alt="menu" class="mb-5 mt-3">
    <img src="../assets/community.svg" alt="menu" class="mb-5">
    <img src="../assets/book.svg" alt="menu" >
    </div>
</div>
</template>

<script>
export default {
  name: "navbar",
  props: ["pageToShow"],
};
</script>

<style lang="scss" scoped>
.body {
  background-color: #a4a4a4;
  height: 100vh;
  width: 100px;
}

.navGroup{
  top: 0;
  position: absolute;
  text-align: center;

}

img {
 width: 2em;
 margin: 1em;
 cursor: pointer;
}




</style>