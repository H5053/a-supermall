<template>

    <div id="tab-bar">
      <!-- slot插槽 -->
      <slot></slot>
    </div>

</template>

<script>

export default {
  name: 'TabBar',
}
</script>

<style>
  #tab-bar{
    display: flex;
    background-color: #f6f6f6;
    /**position定位 */
    position: fixed;
    left: 0;
    right: 0;
    bottom: 0;
    /**阴影过度 */
    box-shadow:0px -1px 7px #888888;
  }

  
</style>