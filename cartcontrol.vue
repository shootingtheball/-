<template>
  <div class="cartcontrol">
    <transition name="move">
    <div class="cart-decrease "  v-show="food.count>0" @click="decreaseCart">
        <transition name="move2" v-show="food.count>0">
        <span v-show="food.count>0" class="fa fa-minus-circle"></span>
        </transition>
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
              this.food.count +=1
          }
         console.log(1)
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
}
.cart-add,.cart-decrease{
    display:inline-block;
    padding: 6px;
    font-size: 24px;
    line-height: 24px;
    width: 24px;
    height: 24px;
    color:#00a0dc;
}
.move-enter-active{
    transition: all 0.4s linear
}
.move-leave-active{
    transition: all 0.4s linear
}
.move-enter,.move-leave-to{
    opacity: 0;
    transform: translate(20px)
}
.move2-enter,.move2-leave-to{
    color: red;
    transform: rotate(180deg)
}
.move2-enter-active{
    transform: all 0.4s linear;
}
.move2-leave-active{
    transform: all 0.4s linear;
}
.cart-decrease span{
    display: inline-block;
}
</style>


