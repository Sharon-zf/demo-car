<template>
  <div class="app-container">
    <!-- 头部区域 -->
    <Header title="购物车案例"></Header>
    <!-- 循环渲染商品 -->
    <!-- v-for循环数组，:key维护列表的状态,通过父向子传值渲染页面 -->
    <Goods
      v-for="item in list"
      :key="item.id"
      :id="item.id"
      :title="item.goods_name"
      :pic="item.goods_img"
      :price="item.goods_price"
      :state="item.goods_state"
    ></Goods>
  </div>
</template>

<script>
//引入组件
import Header from "@/components/Header/Header.vue";
import Goods from "@/components/Goods/Goods.vue";
import axios from "axios";

export default {
  data() {
    return {
      //存储购物车数据的列表，默认为空1
      list: [],
    };
  },
  created() {
    this.initCartList();
  },
  methods: {
    async initCartList() {
      //获取商品数据
      const { data: res } = await axios.get("https://www.escook.cn/api/cart");
      if (res.status === 200) {
        this.list = res.list;
      }
    },
  },
  //注册组件
  components: {
    Header,
    Goods,
  },
};
</script>

<style lang="less" scoped>
.app-container {
  padding-top: 45px;
  padding-bottom: 50px;
}
</style>
