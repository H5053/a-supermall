<template>
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BScroll, { ObserveDom } from 'better-scroll'

export default {
  name: "Scroll",
  props: {
    probeType: {
      type: Number,
      default: 0
    },
    pullUpLoad: {
      type: Boolean,
      default: false
    }
  },
  data() {
    return {
      scroll: null
    }
  },
  mounted() {
    //通过querySelector获取的元素可能不准确，不推荐使用,推荐使用ref
    // this.scroll = new BScroll(document.querySelector(".wrapper"), {})

    this.scroll = new BScroll(this.$refs.wrapper, {
      click: true,  //允许监听点击
      probeType: this.probeType,
      pullUpLoad: this.pullUpLoad,
      ObserveDom: true,
      observeImage: true
    })

    // 监听上拉
    this.scroll.on('scroll', (position) => {
      this.$emit('scroll', position)
    })

    // // 上拉加载更多
    // this.scroll.on('pullingUp', () =>{
    //   // 发送网络请求，请求更多页的数据
    //   // 等数据请求完成，并将新的数据展示出来后 bscroll.finishPullUp() 才会允许下一次下拉加载更多
    //   this.$emit('pullingUp')
    // })
    console.log(this.scroll)
    this.scroll.refresh()
  },
  methods: {
    scrollTo(x, y, time=500) {
      this.scroll.scrollTo(x, y, time)
    },
    finishPullUp() {
      this.scroll.finishPullUp()
    },
    refresh() {
      this.scroll.refresh()
    }

  }
}
</script>

<style>

</style>