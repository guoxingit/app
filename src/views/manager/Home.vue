<template>
  <div class="home">
    <header class="header">
      <img src="../../assets/home.jpg" alt="">
      </header>
      <!-- 内容区 -->
      <div>
        <!-- 分类 -->
        <van-grid :column-num="3">
        <van-grid-item
          v-for="value in categories"
          :key="value.id"
          :icon="value.icon"
          :text="value.name"
        />
        </van-grid> 
        <!-- 产品 -->
        <briup-product-item 
        @click="toBuyHandler(p)"
        v-for="p in products"
        :key="p.id" 
        :data="p">
      </briup-product-item>
      </div>
    
   
  </div>
</template>
<script>
import {get,post} from '../../http/axios';        // import {mapState, mapActions} from 'vuex'
export default {
  data(){
    return{
      categories:[],
      products:[]
    }
  },
  
  created(){
    //查询栏目
    this.loadcategories();
    //查询产品
    this.loadproducts();
  },
  methods:{
    toBuyHandler(p){
      //alert(JSON.stringify(p));
      this.$router.push({
        path:"/manager/order_confirm",
        query:p
      })
    },
    //加载栏目信息
    loadcategories(){
      let url="/category/findAll";
      get(url).then((response)=>{
        this.categories=response.data.slice(0,6);
      })
    },
    loadproducts(){
      let url="/product/query";
      let params={
        page:0,
        pageSize:100
      }
      post(url,params).then((response)=>{
          this.products=response.data.list;
      })
    }
  }
}
</script>
<style scoped>
.home {
  padding-bottom: 50px;
}
.header {
  height: 300px;
  overflow: hidden;
}
.header img {
  width: 100%;
}
</style>