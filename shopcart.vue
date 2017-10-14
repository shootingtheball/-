<template>
  <div class="shopcart">
      <div class="content" @click="toggleList">
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
      <transition name="list-move">
      <div class="shopcart-list" v-show="listShow">
          <div class="list-header">
              <div class="list-title">购物车</div>
              <div class="empty">清空</div>
          </div>
          <div class="list-content" ref="pr">
              <ul>
                  <li v-for="item in selectFoods">
                      <div class="name">{{item.name}}</div>
                      <div class="price">{{item.price}}</div>
                      <div class="cartcontrol-wrapper" > 
                          <cartcontrol :food="item" class="cartcontrol"></cartcontrol>
                      </div>
                  </li>
              </ul>
          </div>
      </div>
      </transition>
     <!-- <transition name="fade">
          <div class="mask" v-show="listShow"></div>
      </transition> -->
  </div>
</template>

<script>
import BScroll from "better-scroll";
import cartcontrol from"../cartcontrol/cartcontrol";
import Vue from "vue";

export default {
  name:"shopcart",
  data() {
      return{
          fode:false
      }
  },
  props:{
      minPrice:{
          type:Number,
          default:0
      },
      selectFoods:{
          default() {
              return [];
          }
      }
  },
  mounted() {
      console.log(1)
              
  },
  methods:{
      initScroll() {
                this.HAHA= new BScroll(this.$refs.pr,{click:true});
            },
      toggleList() {
          if(this.selectFoods.length===0){
              return false
          }else{
              this.fode = !this.fode;

          }
      }
  },
  components:{
      cartcontrol
  },
  computed:{
      totlePrice() {
          var totle =0;
          this.selectFoods.forEach(function(f) {
            totle += f.count*f.price
          });
          if(this.fode){
              if(!this.HAHA){
                         this.$nextTick(function(){
                  this.initScroll(); 
              })
              }else{

              }
          }
          return totle;
         
      },
      listShow() {
          if(this.selectFoods.length===0){
              this.fode=false
          };
          return this.fode;
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
    color: gray; 
}
.content{
    display: flex;
    background: #141d27;
    position: absolute;
    width: 100%;
    z-index: 10;
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
    line-height: 44px;
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

.list-content .name{
    font-weight: 700;
    font-size: 14px;
    flex:1
}
.list-header{
    display: flex;
    justify-content: space-between;
    padding:  0 20px;
    background: #f3f5f7;
}
.list-content ul{
    padding: 0 20px;
    background: #fff;
    max-height: 150px;
}
.list-content li{
    display: flex;
    border-bottom: 1px solid rgba(7, 17, 27,0.2);
    height: 48px;
    justify-content: space-between;
}
.list-content li div{
    line-height: 48px
}
.cartcontrol-wrapper{
    vertical-align: baseline;
}
.cartcontrol{
    vertical-align: baseline;
    height: 48px;
}
.shopcart-list{
    color: black;
    position: absolute;
    top: 0;
    z-index: 50;
    left: 0;
    width: 100%;
    transform: translate3d(0, -100%, 0)
}
.list-move-enter-active,.list-move-leave-active{
    transition: all 0.3s linear;
}
.list-move-enter,.list-move-leave-to{
transform: translate3d(0, 0, 0)
}
.mask{
    position: fixed;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background: rgba(7, 17, 27, .6);
    z-index: 2000;
}
</style>
