<template>
	<div class="cartcontrol">
	  <transition name="move">
	    <div class="cart-decrease" v-show="food.count>0" @click.prevent.stop="descreaseCart">
	      <span class="inner icon-remove_circle_outline"></span>
	    </div>
	  </transition>
    <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
    <div class="cart-add icon-add_circle" @click.prevent.stop="addCart"></div>
	</div>
</template>

<script type="text/ecmascript-6">
import Vue from 'vue';

export default {
  props: {
    food: {
      type: Object
    }
  },
  methods: {
    addCart(event) {
      if (event._constructed ? 0 : 1) {
        return;
      }
      if (!this.food.count) {
        Vue.set(this.food, 'count', 1);
      } else {
        this.food.count++;
      }
        this.$emit('addCart', event.target);
    },
    descreaseCart(event) {
      if (event._constructed ? 0 : 1) {
        return;
      }
      if (this.food.count) {
        this.food.count--;
      }
    }
  }
};
</script>

<style lang="stylus" rel="stylesheet/stylus">
  .cartcontrol
    font-size: 0
    .cart-decrease
      display: inline-block
      padding: 6px
      transition: all 0.4s linear
      &.move-enter-active
        opacity: 1
        transform: translate3d(0, 0, 0) rotate(0)
      .inner
        line-height: 24px
        font-size: 24px
        color: rgb(0, 160, 220)
      &.move-enter, &.move-leave-active
        opacity: 0
        transform: translate3d(24px, 0, 0) rotate(180deg)
    .cart-count
      display: inline-block
      font-size: 10px
      line-height: 24px
      width: 12px
      vertical-align: top
      padding-top: 6px
      text-align: center
      color: rgb(147, 153, 159)
    .cart-add
      display: inline-block
      padding: 6px
      line-height: 24px
      font-size: 24px
      color: rgb(0, 160, 220)
</style>