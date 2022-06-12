<template>
<div  class="body">
  <div class="navGroup">
    <img src="../assets/menu.svg" alt="menu" class="mb-5 mt-4">
    <img src="../assets/book.svg" alt="book" class="mb-5" >
        <img src="../assets/community.svg" alt="community" >
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
  background-color: #D9D9D9;
  height: 100vh;
  width: 100px;
  border:solid;
  border-left: none;
  border-top: none;
  border-bottom: none;
  border-width: 2px;
  border-color: rgba(0, 0, 0, 0.158);
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