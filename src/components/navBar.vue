<template>
  <div class="body">
    <div class="navGroup">
      <img src="../assets/menu.svg" alt="menu" :class="menuActive ? 'active' : ''" class="mb-5 mt-4" @click="gotoMenu">
      <img src="../assets/book.svg" alt="book" :class="bookActive ? 'active' : ''" class="mb-5" @click="gotoBook">
      <img src="../assets/community.svg" alt="community" :class="communityActive ? 'active' : ''"
        @click="gotoCommunity">
    </div>
  </div>
</template>

<script>
export default {
  name: "navbar",
  props: ["pageToShow", "menuActive", "bookActive", "communityActive"],

  methods: {
    gotoMenu() {
      this.$emit('gotoMenu')
    },
    gotoBook() {
      this.$emit('gotoBook')
    },
    gotoCommunity() {
      this.$emit('gotoCommunity')
    }
  }
};
</script>

<style lang="scss" scoped>
.body {
  background-color: #121212;
  height: 100vh;
  width: 100px;
  border: solid;
  border-left: none;
  border-top: none;
  border-bottom: none;
  border-width: 2px;
  border-color: rgba(0, 0, 0, 0.158);
}

.navGroup {
  top: 0;
  position: absolute;
  text-align: center;

}

img {
  width: 2em;
  margin: 1em;
  cursor: pointer;
  filter: invert(100%) sepia(0%) saturate(1046%) hue-rotate(138deg) brightness(100%) contrast(10%);
}

.active {
  filter: invert(62%) sepia(34%) saturate(2921%) hue-rotate(218deg) brightness(100%) contrast(98%);
}



img:hover {
  filter: invert(100%) sepia(0%) saturate(7456%) hue-rotate(108deg) brightness(116%) contrast(105%);
}
</style>