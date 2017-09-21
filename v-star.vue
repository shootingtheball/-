<template>
  <div class="vStar" :class="detialStar">
    <template>
      <span v-for="star in stars" class="vStars" >
      <img :src="star.picture">
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
      this.stars=this.stars.splice(0,this.stars.length);
      console.log(this.stars.length)
      for (var i = 0; i< integer; i++) {
        this.stars.push({picture:picStar}) 
      }
      
      if (compare>=0) {
        this.stars.push({picture:picStar2})
      }
    }
  }
}
</script>

<style>
.vStar{
  border: 1px solid yellow
}
.vStars img{
  width: 100px;
}
</style>

