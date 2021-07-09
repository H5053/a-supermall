<template>
  <div class="recommend">
    <div v-for="item in recommends" :key="item">
      <a :href="item.link">
        <img :src="item.image" alt="">
        <div>{{item.title}}</div>
      </a>
    </div>
  </div>
</template>

<script>
export default {
  name: "RecommendView",
  props: {
    recommends: {
      type: Array,
      default() {
        return []
      }
    }
  }
}
</script>

<style>
  .recommend {
    display: flex;
    width: 100%;
    text-align: center;
    font-size: 12px;
    padding: 15px 0 20px 0;
    border-bottom: 8px solid #eee;
  }
  .recommend img{
    width: 90%;
    margin-bottom: 10px;
  }

</style>