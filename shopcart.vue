<template>
  <div class="shopcart">
      <div class="content">
      <div class="content-left">
          <div class="logo-wrapper">
              <div class="logo fa fa-cart-plus" :class="{highlight:totlePrice>0}">
              </div>
              <div class="num" v-show="totlePrice>0"></div>
          </div>
          <div class="price" :class="{highlight2:totlePrice>0}">
              {{totlePrice}}元
          </div>
          <div class="desc">
              另需配送费{{minPrice}}
          </div>
      </div>
      <div class="content-right" >
          <div class="pay"  :class="payClass">{{payDesc}}</div>
      </div>
      </div>
  </div>
</template>

<script>
import Vue from "vue";

export default {
  name:"shopcart",
  props:{
      minPrice:{
          type:Number,
          default:0
      },
      select:{
          type:Array,
          default() {
              return [{price:10,count:1}]
          }
      },
      goods:{
          type:Object
      }
  },
  computed:{
      totlePrice() {
          var totle =0;
          this.select.forEach(function(f) {
            totle += f.count*f.price
          });
          return totle;
      },
      payDesc() {
          if (this.totlePrice===0){
              return `还差${this.minPrice}元起送`
          }else if(this.totlePrice<this.minPrice){
              let diff = this.minPrice - this.totlePrice;
              return `还差￥${diff}元`
          }else{
              return "去结算"
          }
      },
      payClass() {
          if (this.totlePrice>this.minPrice) {
              return "enough"
          }
      }
  },
  created() {
      this.selectFoods();
  },
  methods:{
      selectFoods() {
          var d = [1,2,3];
          console.log(this.goods);
             var data=[];
             console.log(Array.isArray(this.goods));
              this.goods.forEach(function(element) {
                  element.foods.forEach(function(ele){
                      if(ele.count){
                          console.log(ele);
                          data.push(ele)
                      }
                  })
              });
              console.log(data);
              return data;
      }
  }
}
</script>

<style scoped>
.pay span{
    display: inline-block;
    color: black;
    width: 20px;
    height: 20px;
}
.shopcart{
    position: fixed;
    left: 0;
    bottom: 0;
    z-index: 100;
    width: 100%;  
    height: 48px;
    line-height: 48px;
    color: gray
}
.content{
    display: flex;
    background: #141d27;
}
.content-left{
    flex: 1;
    font-size: 0
}
.logo-wrapper{
    vertical-align: middle;
    vertical-align: top;
    display: inline-block;
    font-size: 16px;
    position: relative;
    top: -10px;
    box-sizing: border-box;
    height: 56px;
    width: 56px;
    border-radius: 50%;
    background: #141d27;
    padding: 6px;
    margin: 0 12px;
}
.logo{
    width: 100%;
    height: 100%;
    border-radius: 50%;
    background: #2b343c;
    text-align: center;
    height: 44px;
    cursor: pointer;
    font-size: 24px
}
.logo i{
    color: #80858a;
    line-height: 50px;
    font-size: 24px
}
i img{
    width: 60%;
}
.price,.desc{
    display: inline-block;
}
.content-right{
    width: 100px;
    cursor: pointer;
}
.price{
    vertical-align: top;
    line-height: 48px;
    padding-right: 12px;
    box-sizing: border-box;
    font-size: 16px;
    height: 48px;
}
.desc{
    vertical-align: top;
    font-size: 16px;
    font-size: 10px;
    margin: 0 0 0 12px;
    line-height: 48px;
    height: 48px;
}
.pay{
    font-size: 12px;
    height: 48px;
    line-height: 48px;
    text-align: center;
    font-weight: 700;
    background: #2b333b;
}
.num{
    position: absolute;
    top: 0;
    right:0;
    width: 24px;
    height: 16px;
    line-height: 16px;
    text-align: center;
    font-size: 16px;
    color: red;
    font-weight: 700;
    border-radius: 16px;
    background: rgb(240,20,20);
    box-shadow:  0 4px 8px 0 rgba(0, 0, 0,0.4)
}
.highlight{
    background: rgb(0,160,220);
    color: #fff
}
.highlight2{
    color: #fff
}
.enough{
    background: #00b43c;
    color: #fff
}
</style>
