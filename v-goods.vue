<template>
  <div class="goods">
      <div class="goods-menu">
          <ul>
              <li v-if="goods" v-for="item in goods" class="menu-item"><span>{{item.name}}</span></li>
          </ul>
      </div>
      <div class="goods-food" ref="pro">
          <ul class="goods-ul">
              <li v-for="item in goods"  >
                  <h1>{{item.name}}</h1>
                  <ul class="foods-ul">
                      <li v-for="n in item.foods" class="foods-item">
                          <div class="icon"><img src="./1.jpeg" width="100px"></div>
                          <div class="foods-content">
                              <div v-if="n.description">{{n.description}}</div>
                              <div>{{n.name}}</div>
                              <div>{{n.price}}</div>
                          </div>
                      </li>
                  </ul>
              </li>
          </ul>
      </div>
  </div>
</template>

<script>
import BScroll from "better-scroll";

export default {
  name:"vGoods",
  data() {
      return{
        goods:"",
        scrollY,
        height
      }
  },
        created() {
			this.$http.get('api/goods').then((response) => {
				response=response.body;
				if (response.errno ===0) {
					this.goods = response.data;
				}
            }),
            this.$nextTick(() => {
                this.haha = new BScroll(this.$refs.pro,{type:3});
                this.haha.on("scroll",(pos) => {
                    this.scrollY = Math.abs(Math.round(pos.y))
                })
            })
        },
        methods:{
            caculateH() {
                var dataLi = this.$refs.pro.getElementsByTagName("li");
                this.height = 0;
                var data =[0];
                for (var i = 0; i < dataLi.length; i++) {
                    height += dataLi[i].clientHeight;
                    data.push(height);
                    }
                }
            },
        computed:{
            currentIndex() {
                for (var i = 0; i < this.length; i++) {
                    var element = this.length[i];
                    var element2 =this.length[i+1];
                if(!height2||this.scrollY>element && this.scrollY<element2){
                    return i 
                }
            }
            }
        }
}
</script>

<style>
.goods{
    overflow: hidden;
    display: flex;
    position: absolute;
    width: 100%;
    top:135px;
    bottom: 48px;
    z-index: -1;
}
.goods-menu{
    flex: 0 0 80px;
    width: 80px;
    background: #F5F5F5;
}
.goods-food{
    flex: 1
}
.menu-item{
    text-align: center;
    font-size: 12px;
    height: 54px;
    display: table;
    width: 56px;
    position: relative;
    padding:0 12px
}
.menu-item:hover{
    background:	#fff
}
.menu-item span{
    display: table-cell;
    vertical-align: middle;
}
.menu-item::after{
    content: "";
    position: absolute;
    left: 12px;
    right: 12px;
    bottom: 0;
    border-bottom: 1px solid rgba(7, 17, 27, .1)
}
li{
    list-style:  none;
}
.goods-food h1{
    font-size: 12px;
    height: 26px;
    line-height: 26px;
    background: #f3f5f7;
    color:#93999f;
    border-left: 2px solid #d9dde1;
    padding-left: 12px
}
.foods-content{
    margin:0 18px;
    font-size:14px;
    font-weight: 400;
    flex: 1
}
.foods-item{
        display: flex;
        height: 78px;
        padding: 18px 0;
        margin: 0 18px;
        border-bottom: 1px solid rgba(7, 17, 27, .1);
}
.foods-ul li:last-child{
    border:0
}

.icon{
    flex : 0 0 57px;
}
.foods-item img{
    width: 63px
}
</style>
