<template>
  <div
    class="number-container d-flex justify-content-center align-items-center"
  >
    <!-- 减 1 的按钮 -->
    <button type="button" class="btn btn-light btn-sm" @click="sub">-</button>
    <!-- 购买的数量 -->
    <span class="number-box">{{ num }}</span>
    <!-- 加 1 的按钮 -->
    <button type="button" class="btn btn-light btn-sm" @click="add">+</button>
  </div>
</template>

<script>
//引入EventBus
import bus from "@/components/eventBus.js";

export default {
  props: {
    //商品的数量
    num: {
      default: 1,
      typeof: Number,
    },
    //商品的id
    id: {
      required: true,
      typeof: Number,
    },
  },
  methods: {
    //通过计算属性将num加减然后用eventbus将数据交给根组件
    add() {
      const obj = { id: this.id, value: this.num + 1 };
      bus.$emit("share", obj);
    },
    sub() {
      if (this.num - 1 === 0) return;
      const obj = { id: this.id, value: this.num - 1 };
      bus.$emit("share", obj);
    },
  },
};
</script>

<style lang="less" scoped>
.number-box {
  min-width: 30px;
  text-align: center;
  margin: 0 5px;
  font-size: 12px;
}

.btn-sm {
  width: 30px;
}
</style>
