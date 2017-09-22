<template>
  <div class="main" :class="detialStar">
      <span v-for="item in stars" class="wraper" :key="item.id" >
      <img :src="item.vSrc" :style="starStyle">
      </span>
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
      this.stars.splice(0,this.stars.length);

      for (var i = 0; i< integer; i++) {
        this.stars.push({vSrc:picStar,
        id:i+1}) 
      }
      
      if (compare>=0) {
        this.stars.push({vSrc:picStar2})
        this.stars=this.stars.splice(0,this.stars.length);
      }
    },
    starStyle() {
      return {
        width:this.size+"px"
      }
    }
  }
}
</script>

<style>

.main{

}
.wraper{
  margin-right: 5%;
}
.wraper:last-child{
  margin-right: 0;
}
</style>

