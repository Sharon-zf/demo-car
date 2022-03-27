<template>
  <div class="app-container">
    <!-- 头部区域 -->
    <Header title='购物车案例'></Header>
    <h1>App 根组件</h1>
  </div>
</template>

<script>
import Header from '@/components/Header/Header.vue'
import axios from 'axios'
export default {
  created(){
    this.initCartList()
  },
  methods: {
    async initCartList(){
      const {data:res} = await axios.get('https://www.escook.cn/api/cart')
      console.log(res)
    }
  },
  components: {
    Header
  }
}
</script>

<style lang="less" scoped>
.app-container {
  padding-top: 45px;
  padding-bottom: 50px;
}
</style>
