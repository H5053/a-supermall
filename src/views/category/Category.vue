<template>
  <div id="category">
    <nav-bar class="home-nav"><template v-slot:center>分类</template></nav-bar>
  </div>
</template>

<script>
  import NavBar from 'components/common/navbar/NavBar.vue'
  export default {
    name: "category",
    components: {
      NavBar
    },
  }
</script>

<style scoped>
  .home-nav {
    background-color: var(--color-tint);
    color: white;
  }
</style>