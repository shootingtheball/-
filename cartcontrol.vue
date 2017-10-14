<template>
  <div class="cartcontrol">
    <transition name="move">
    <div class="cart-decrease "  v-show="food.count>0" @click="decreaseCart">
        <span  class="inner fa fa-minus-circle"></span>
    </div>
    </transition>
    <div class="cart-count" v-show="food.count>0">{{food.count}}</div>
    <div class="cart-add fa fa-plus-circle" @click="addcart"></div>
  </div>
</template>

<script>
import Vue from "vue";
export default {
  props:{
      food:{
          type:Object
      }
  },
  methods:{
      addcart(event) {
          if(!event._constructed){
              return;
          }
          if(!this.food.count){
              Vue.set(this.food,"count",1)
          }else{
              this.food.count +=1;
          }
          this.$emit("increment")
      },
      decreaseCart() {
          if(!event._constructed){
              return;
          }
          if(this.food.count>0){
              this.food.count --
          }
      }
  }
}
</script>

<style scoped>
.cartcontrol{
    font-size: 0;
    
}
.cart-count{
    display:inline-block;
    vertical-align: top;
    padding-top: 6px;
    line-height: 24px;
    width: 12px;
    text-align: center;
    color: #93999f;
    font-size:10px;
    transform: translate3d(0, 0, 0)
}
.cart-add,.cart-decrease{
    display:inline-block;
    padding: 6px;
    font-size: 30px;
    line-height: 24px;
    width: 24px;
    height: 24px;
    color:#00a0dc;
    z-index: 1;
}
.move-enter-active{
    transition: all 0.4s linear;
}
.move-leave-active{
    transition: all 0.4s linear;
}
.move-enter,.move-leave-active{
    opacity: 0;
    transform: translate3d(24px, 0, 0)
}
.cart-decrease span{
    display: inline-block;
    transform: rotate(0deg);
    transition: all 0.4s linear;
}
</style>
