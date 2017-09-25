<template>
  <div class="goods">
      <div class="goods-menu">
          <ul>
              <li></li>
          </ul>
      </div>
      <div class="goods-food"></div>
  </div>
</template>

<script>
export default {
  name:"vGoods",
  data() {
      return{
          goods:""
      }
  },
 /* created() {
      this.$http.get("api/goods").then((response)=>{
          response = response.body
          if(response.errno===0){
              this.goods= response.data
          }
      })
  } */
}
</script>

<style>
.goods{
    display: flex;
    position: absolute;
    width: 100%;
    top:400px;
    bottom: 100px;
    z-index: -1;
}
.goods-menu{
    flex: 0 0 120px;
    width: 120px;
    background: #EDEDED;

}
.goods-food{
    flex: 1
}
</style>

