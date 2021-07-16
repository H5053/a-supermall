<template>
  <div class="goods-item">
    <img :src="goodsItem.show.img" alt="" @load="imageLoad">
    <div class="goods-info">
      <!-- 介绍 -->
      <p>{{goodsItem.title}}</p>
      <!-- 价格 -->
      <span class="price">{{goodsItem.price}}</span>
      <!-- 收藏 -->
      <span class="cfav">{{goodsItem.cfav}}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: "GoodsListItem",
  props: {
    goodsItem: {
      type: Object,
      default() {
        return []
      }
    }
  },
  methods: {
  //   imageLoad() {
  //     this.$bus.$emit('itemImageLoad')
  //   }
  }
}
</script>

<style>
  .goods-item {
    padding-bottom: 40px;
    position: relative;
    width: 48%;
  }

  .goods-item img {
    width: 100%;
    border-radius: 5px;
  }

  .goods-info {
    font-size: 12px;
    position: absolute;
    bottom: 5px;
    left: 0;
    right: 0;
    
    /* 内容会被修剪，并且其余内容是不可见的。 */
    overflow: hidden;
    text-align: center;
  }

  .goods-info p {
    overflow: hidden;
    text-overflow: ellipsis;
    /* 文本不会换行 */
    white-space: nowrap;
    margin-bottom: 3px;
  }

  .goods-info .price {
    color: var(--color-high-text);
    margin-right: 20px;
  }

  .goods-info .cfav {
    position: relative;
  }

  .goods-info .cfav::before {
    content: '';
    position: absolute;
    left: -13px;
    top: -1px;
    width: 14px;
    height: 14px;
    background: url("~assets/img/common/collect.svg") 0 0/14px 14px;
  }
</style>