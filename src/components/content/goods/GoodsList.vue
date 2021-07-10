<template>
  <div class="goods">
      <GoodsListItem v-for="(item, index) in goods" :key="index" :goodsItem="item"></GoodsListItem>
  </div>
</template>

<script>

import GoodsListItem from './GoodsLIstItem.vue'

export default {
    props: {
        goods: {
            type: Array,
            default() {
                return []
            }
        }
    },
    components: {
        GoodsListItem
    }
}
</script>

<style>
.goods {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-around;
    padding: 2px;
  }
</style>