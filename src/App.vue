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
      @state-change="getNewState"
      :count="item.goods_count"
    ></Goods>
    <Footer
      :amount="amt"
      :isFull="fullState"
      @full-change="getFullChange"
      :number="number"
    ></Footer>
  </div>
</template>

<script>
//引入组件
import Header from "@/components/Header/Header.vue";
import Goods from "@/components/Goods/Goods.vue";
import Footer from "@/components/Footer/Footer.vue";
//引入axios
import axios from "axios";

import bus from "@/components/eventBus.js"

export default {
  data() {
    return {
      //存储购物车数据的列表，默认为空
      list: [],
    };
  },
  //计算属性
  computed: {
    //判断所有的商品的状态是否都是选中的状态，若是则将footer组件中的全选框选中
    fullState() {
      //this方法与some方法类似，若所有数据运行函数后结果均为true则返回true
      return this.list.every((item) => item.goods_state);
    },
    //通过计算属性计算出已选商品的总价
    amt() {
      return (
        this.list
          //filter：过滤状态为true的商品
          //fliter：返回运行函数后返回值为true的元素组成的数组
          .filter((item) => item.goods_state)
          //reduce：接收一个函数作为累加器，数组中的每个值（从左到右）开始相加最终为一个值
          .reduce(
            (total, item) => (total += item.goods_price * item.goods_count),
            0
          )
      );
    },
    number(){
      return (
        this.list.filter(item => item.goods_state)
        .reduce(
        (number,item) =>(number += item.goods_count),0
        )
      );
    }
  },
  created() {
    this.initCartList();
    bus.$on("share",val=>{
      this.list.some(item=>{
        if(item.id===val.id){
          item.goods_count=val.value
          return true
        }
      })
    })
  },
  methods: {
    async initCartList() {
      //获取商品数据
      const { data: res } = await axios.get("https://www.escook.cn/api/cart");
      if (res.status === 200) {
        this.list = res.list;
      }
    },
    //state-change自定义事件触发后执行此函数
    getNewState(e) {
      //some方法：对数组中每个元素运行给定函数，如果任一元素返回true，则返回true停止遍历。
      this.list.some((item) => {
        //遍历数组，寻找请求的数据中id与点击的id相同的数据然后将复选框目前的状态赋值给数据
        if (item.id === e.id) {
          item.goods_state = e.value;
          return true;
        }
      });
    },
    //触发自定义事件full-change后将获取到的全选框的状态渲染到每个item中
    getFullChange(e) {
      this.list.forEach((item) => {
        item.goods_state = e;
      });
    },
  },
  //注册组件
  components: {
    Header,
    Goods,
    Footer,
  },
};
</script>

<style lang="less" scoped>
.app-container {
  padding-top: 45px;
  padding-bottom: 50px;
}
</style>
