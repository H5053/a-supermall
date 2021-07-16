<template>
  <div id="home">
    <nav-bar class="home-nav"><template v-slot:center>购物街</template></nav-bar>
    
    <scroll class="content" ref="scroll" :probe-type="3" @scroll="contentScroll" :pull-up-load="true"> 
      <home-swiper :banners="banners"/>
      <recommend-view :recommends="recommends"/>
      <feature-view/>
      <tab-control class="tab-control" :titles="['流行', '新款', '精选']" @tabClick="tabClick"/>
      <goods-list :goods="showGoods" />
    </scroll>

    <!-- .native监听组件,vue3.x不需要添加也可以监听 -->
    <back-top @click="backClick" v-show="isShowBackTop"/>

  </div>

</template>

<script>
  import HomeSwiper from './childComps/HomeSwiper.vue'
  import RecommendView from './childComps/RecommendView.vue'
  import FeatureView from './childComps/FeatureView.vue';


  import NavBar from 'components/common/navbar/NavBar.vue'
  import TabControl from 'components/content/tabControl/TabControl.vue';
  import Scroll from 'components/common/scroll/Scroll.vue';
  import GoodsList from 'components/content/goods/GoodsList.vue';
  import BackTop from 'components/content/backtop/BackTop.vue';
  

  import { getHomeMultidata, getHomeGoods} from "network/home.js";



 

  export default {
    name: "Home",
    components: {
      HomeSwiper,
      RecommendView,
      FeatureView,
      GoodsList,

      NavBar,
      TabControl,
      Scroll,
      BackTop,

    },
    data() {
      return {
        banners: [],
        recommends: [],
        goods: {
          'pop': {page: 0, list: []},
          'new': {page: 0, list: []},
          'sell': {page: 0, list: []},
        },
        currentType: 'pop',
        isShowBackTop: false
      }
    },
    computed: {
      showGoods() {
        return this.goods[this.currentType].list
      }
    },
    created() {
      //请求多个数据
      this.getHomeMultidata()
      //请求商品数据
      this.getHomeGoods('pop')
      this.getHomeGoods('new')
      this.getHomeGoods('sell')

      // 监听item中图片加载完成
      // this.$bus.$on('itemImageLoad', () => {
      //    this.$refs.scroll.refresh()
      // })
    },
    methods: {
      backClick() {
        this.$refs.scroll.scrollTo(0, 0)
      },

      //监听上拉
      contentScroll(position) {
        this.isShowBackTop = (-position.y) > 1000
        
      },

      //事件监听
      tabClick(index) {
        switch(index) {
          case 0:
            this.currentType = 'pop'
            break
          case 1:
            this.currentType = 'new'
            break
          case 2:
            this.currentType = 'sell'
            break
        }
      },

      // 网络请求请求封装成方法
      getHomeMultidata() {
        getHomeMultidata().then(res => {
          this.banners = res.data.banner.list;
          this.recommends = res.data.recommend.list;
        })
      },
      getHomeGoods(type) {
        const page = this.goods[type].page + 1
        getHomeGoods(type, page).then(res => {
          this.goods[type].list.push(...res.data.list)
          this.goods[type].page += 1

        })
      }
    }
  }
</script>

<style scoped>
  #home {
    height: 100vh;
    position: relative;
  }

  .home-nav {
    background-color: var(--color-tint);
    color: white;

    /* fixed相对于浏览器绝对定位 */
    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    /* 设置图形堆叠顺序,越大的在前 */
    z-index: 9;
  }

  .tab-control {
    /* 粘性定位 */
    position: sticky;
    top: 44px;
    z-index: 9;
  }

  .content {
    overflow: hidden;
    position:absolute;
    top: 44px;
    bottom: 49px;
    left: 0;
    right: 0;
  }

</style>