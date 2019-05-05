<template>
  <div class="goods">
    <div class="menu-wrapper">
      <ul>
        <li 
          class="menu-item"
          v-for="(item,index) in goods"
          :key="index"
        >
          <span class="text border-1px">
            <span v-show="item.type>0" class="icon" :class="classMap[item.type]"></span>{{item.name}}
          </span>
        </li>
      </ul>
    </div>
    <div class="foods-wrapper">
      <ul>
        <li 
          class="food-list"
          v-for="(item,index) in goods"
          :key="index"
        >
          <h1 class="title">{{item.name}}</h1>
          <ul>
            <li
              class="food-item"
              v-for="(food,index) in item.foods"
              :key="index"
            >
              <div class="icon">
                <img :src="food.icon" alt="">
              </div>
              <div class="content">
                <h2 class="name">{{food.name}}</h2>
                <p class="desc">{{food.description}}</p>
                <div class="extra">
                  <span>月售{{food.sellCount}}份</span>
                  <span>好评率{{food.rating}}%</span>
                </div>
                <div class="price">
                  <span>￥{{food.price}}</span>
                  <span v-show="food.oldPrice">￥{{food.oldPrice}}</span>
                </div>
              </div>
            </li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import { getGoods } from 'api'


export default {
  data() {
    return{
      goods: [],

    }
  },
  props: {
    seller: {
      type: Object
    }
  },
  created() {
    this.classMap = ['decrease','discount','special','invoice','guarantee'];
    
    getGoods().then((goods) => {
      this.goods = goods
    })
  },
}
</script>

<style lang="stylus" rel="stylesheet/stylus">
@import "../../common/stylus/mixin.styl"

  .goods
    display flex
    position absolute
    width 100%
    top 174px
    bottom 46px
    overflow hidden
    .menu-wrapper
      flex 0 0 80px
      width 90px
      background #f3f5f7
      .menu-item
        display table
        height 54px
        width 56px
        line-height 14px
        padding 0 12px
        .icon
          display inline-block
          vertical-align top 
          width 12px
          height 12px
          margin-right 2px
          background-size 12px 12px
          background-repeat no-repeat
          &.decrease
            bg-image('decrease_3')
          &.discount
            bg-image('discount_3')
          &.guarantee
            bg-image('guarantee_3')
          &.invoice
            bg-image('invoice_3')
          &.special
            bg-image('special_3')
        .text
          font-size 12px
          display table-cell
          width 56px
          vertical-align middle
          border-1px(rgba(7,17,27,0.1))
    .foods-wrapper
      flex 0 0 80px
         
</style>
