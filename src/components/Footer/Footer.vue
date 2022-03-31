<template>
  <div class="footer-container">
    <!-- 左侧的全选 -->
    <div class="custom-control custom-checkbox">
      <input
        type="checkbox"
        class="custom-control-input"
        id="cbFull"
        :checked="isFull"
        @change="fullChange"
      />
      <label class="custom-control-label" for="cbFull">全选</label>
    </div>

    <!-- 中间的合计 -->
    <div>
      <span>合计：</span>
      <!-- toFixed(n):保留n为小数 -->
      <span class="total-price">￥{{ amount.toFixed(2) }}</span>
    </div>

    <!-- 结算按钮 -->
    <button type="button" class="btn btn-primary btn-settle">
      结算 ({{ number }})
    </button>
  </div>
</template>

<script>
export default {
  props: {
    //渲染全选框的状态
    isFull: {
      default: false,
      typeof: Boolean,
    },
    //渲染总价
    amount: {
      default: 0,
      typeof: Number,
    },
    //渲染已勾选的商品数量
    number: {
      default:0,
      typeof:Number,
    }
  },
  methods: {
    //监听全选框的状态，并获取
    fullChange(e) {
      this.$emit("full-change", e.target.checked);
    },
  },
};
</script>

<style lang="less" scoped>
.footer-container {
  font-size: 12px;
  height: 50px;
  width: 100%;
  border-top: 1px solid #efefef;
  position: fixed;
  bottom: 0;
  background-color: #fff;
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0 10px;
}

.custom-checkbox {
  display: flex;
  align-items: center;
}

#cbFull {
  margin-right: 5px;
}

.btn-settle {
  height: 80%;
  min-width: 110px;
  border-radius: 25px;
  font-size: 12px;
}

.total-price {
  font-weight: bold;
  font-size: 14px;
  color: red;
}
</style>
