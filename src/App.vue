<template>
  <div id="app">
    <v-header :seller="seller"></v-header>
    <div class="tab">
      <div class="tab-item">
        <router-link to='/goods'>商品</router-link>
      </div>
      <div class="tab-item">
        <router-link to='/ratings'>评论</router-link>
      </div>
      <div class="tab-item">
        <router-link to='/seller'>商家</router-link>
      </div>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
import header from './components/header/header.vue'
import { getSeller } from 'api'

const ERR_OK = 0;


export default {
  name: 'App',
  data() {
    return {
      seller:{}
    }
  },
  created() {
    getSeller().then((seller) => {
      this.seller = seller
    })
  },
  components: {
    'v-header': header
  }
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .tab
    display: flex
    width 100%
    height 40px
    line-height 40px
    .tab-item
      flex 1
      text-align center
      & > a
        display block
        text-decoration none
        font-size 14px
        color rgb(77,85,93)
        &.active
          color rgb(240,20,20)
</style>
