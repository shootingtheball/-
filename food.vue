<template>
<transition name="move">
  <div v-show="showFlag" class="food" ref="BS">
    <div class="food-content">
      <div class="img-header">
        <img :src="food.image" alt="">
        <div @click="hide"><i class="fa fa-arrow-left"></i></div>
      </div>
      <div class="content">
        <div class="title"></div>
        <div class="detial"><span>月售{{food.sellCount}}</span><span>好评率{{food.rating}}</span></div>
      </div>
    </div>
  </div>
</transition>
</template>

<script>
import BScroll from "better-scroll";

export default {
  data() {
    return {
      showFlag :false
    }
  },
  props:{
    food:{
      type:Object
    }
  },
  methods:{
    show() {
      this.showFlag = true;
      this.$nextTick(() => {
        if(!this.scroll){
          this.scroll = new BScroll(this.$refs.BS,{click:true})
        }
      })
    },
    hide() {
      this.showFlag = false;
    }
  }
}
</script>

<style scoped>
.food{
  position: fixed;
  left: 0;
  top: 0;
  bottom: 48px;
  width: 100%;
  z-index: 300 ;
  background: #fff;
}
.move-enter-active,.move-leave-active{
  transition: all 0.5s linear
}
.move-leave{
  transform: translate3d(0,0,0)
}
.move-enter,.move-leave-to{
  transform: translate3d(100%,0,0)
}
.food-content{
  height: 100%;
}
.img-header{
  position: relative;
  width: 100%;
  height: 0;
  padding-top: 100%
}
.img-header img{
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
}
.img-header  i{
  color: #fff;
  font-size: 1.5rem;
}
.img-header div{
  padding: 5px;
  position: absolute;
  top: 10px;
  left: 10px;
}
.content{
  padding: 18px;
}

</style>
