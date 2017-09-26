<template>
  <div class="goods">
      <div class="goods-menu">
          <ul>
              <li v-if="goods" v-for="item in goods" class="menu-item"><span>{{item.name}}</span></li>
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
		created() {
			this.$http.get('api/goods').then((response) => {
				response=response.body;
				if (response.errno ===0) {
					this.goods = response.data;
				}
			})
		}
}
</script>

<style>
.goods{
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
</style>

