<template>
  <div>
    <nav-bar class="home-nav">
      <template #center>
        <div>购物车</div>
      </template>
    </nav-bar>
  </div>
</template>

<script>

import NavBar from 'components/common/navbar/NavBar.vue'
import { getHomeMultidata } from "network/home.js";

export default {

  components: {
    NavBar
  },
  created() {
    getHomeMultidata().then(res =>{
      console.log(res);
    })
  }

}
</script>

<style>
.home-nav {
  background: #ff8198;
  color: #fff;
}
</style>