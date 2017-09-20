<template>
  <div class="vStar" :class="detialStar">
    <template>
      <span v-for="star in stars" class="vStars"  :class="detialStars">
      <img :src="star.picStar">
    </span>
    </template>
  </div>
</template>

<script>
var picStar = require("./star.png");
var picStar2 = require("./star2.png")

export default {
  name:"vStar",
  data (){
    return {
      stars:[]
    }
  },
  props:{
    size:{
      type : Number
    },
    score:{
      type : Number
    }
  },
  computed:{
    detialStar() {
      var compare =this.score-(Math.floor(this.score)+0.5);
      var integer = Math.floor(this.score);

      for (var i = 0; i< integer; i++) {
        this.stars.push({stars:picStar}) 
      }
      
      if (compare>0) {
        this.stars.push({stars:picStar2})
      }
    }
  }
}
</script>
