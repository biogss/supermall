<template>
  <div>
    <nav-bar class="home-nav">
    <template #center>
      <div>首页</div>
    </template>
    </nav-bar>
    <home-swiper :banners = "banners" style="padding-top:44px"></home-swiper>
    <HomeRecommend :recommends="recommends"></HomeRecommend>
    <FeatureView></FeatureView>
    <TabControl :titles="['新款', '流行', '爆款']" @itemClick="itemClick"></TabControl>
    <GoodList :goods="showGoods"></GoodList>
    
  </div>
</template>

<script>

import NavBar from 'components/common/navbar/NavBar.vue'
import TabControl from 'components/content/TabControl.vue'
import GoodList from 'components/content//goods/GoodsList.vue'

import HomeSwiper from './childComponents/HomeSwiper.vue'
import HomeRecommend from './childComponents/HomeRecommend.vue'
import FeatureView from './childComponents/FeatureView.vue'

import { getHomeMultidata, getHomeGoods} from "network/home.js";

export default {

  components: {
    NavBar,TabControl,GoodList,
    HomeSwiper,HomeRecommend,FeatureView
  },
  data() {
    return {
      banners: [],
      recommends: [],
      goods: {
        'pop': {page: 0, list: []},
        'new': {page: 0, list: []},
        'sell': {page: 0,list: []}
      },

      currentItem: 'pop'
        
    }
  },
  created() {
    this.getHomeMultidata()

    this.getHomeGoods('pop')
    this.getHomeGoods('new')
    this.getHomeGoods('sell')
  },
  computed: {
    showGoods() {
      return this.goods[this.currentItem].list
    }
  },
  methods: {

    itemClick(index) {
      switch(index) {
        case 0: 
          this.currentItem = 'pop'
          break
        case 1:
          this.currentItem = 'new'
          break
        case 2:
          this.currentItem = 'sell'
          break
      }
    },

    getHomeMultidata() {
      getHomeMultidata().then(res =>{
        // console.log(res);
        this.banners = res.data.data.banner.list
        this.recommends = res.data.data.recommend.list
      })
    },

    getHomeGoods(type) {
      let page = this.goods[type].page + 1
      getHomeGoods(type, page).then(res => {
        console.log(res)
        this.goods[type].list.push(...res.data.data.list)
        this.goods[type].page += 1
      })
    }
  }

}
</script>

<style>
#home {
    /*padding-top: 44px;*/
    height: 100vh;
    position: relative;
  }

  .home-nav {
    background-color: #ff8198;
    color: #fff;

    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    z-index: 9;
  }

  .tab-control {
    position: sticky;
    top: 44px;
    /* z-index: 9; */
  }

  .content {
    overflow: hidden;

    position: absolute;
    top: 44px;
    bottom: 49px;
    left: 0;
    right: 0;
  }
</style>