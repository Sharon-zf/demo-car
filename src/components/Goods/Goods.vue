<template>
  <div class="goods-container">
    <!-- 左侧图片 -->
    <div class="thumb">
      <div class="custom-control custom-checkbox">
        <!-- 复选框 -->
        <input
          type="checkbox"
          class="custom-control-input"
          id="cb1"
          :checked="state"
        />
        <label class="custom-control-label" for="cb1">
          <!-- 商品的缩略图 -->
          <img :src="pic" alt="" />
        </label>
      </div>
    </div>
    <!-- 右侧信息区域 -->
    <div class="goods-info">
      <!-- 商品标题 -->
      <h6 class="goods-title">{{ title }}</h6>
      <div class="goods-info-bottom">
        <!-- 商品价格 -->
        <span class="goods-price">￥{{ price }}</span>
        <!-- 商品的数量 -->
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    //id作用：以后商品的状态发生改变时需要子向父传值，父组件则根据id修改状态
    id: {
      require: true,
      type: Number
    },
    //要渲染商品的标题
    title: {
      default: "",
      type: String,
    },
    //要渲染商品的图片
    pic: {
      default: "",
      type: String,
    },
    //要渲染商品的价格
    price: {
      default: 0,
      type: Number,
    },
    //要渲染商品的选中状态
    state: {
      default: true,
      type: Boolean,
    },
  },
};
</script>

<style lang="less" scoped>
.goods-container {
  + .goods-container {
    border-top: 1px solid #efefef;
  }
  padding: 10px;
  display: flex;
  .thumb {
    display: flex;
    align-items: center;
    img {
      width: 100px;
      height: 100px;
      margin: 0 10px;
    }
  }

  .goods-info {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    flex: 1;
    .goods-title {
      font-weight: bold;
      font-size: 12px;
    }
    .goods-info-bottom {
      display: flex;
      justify-content: space-between;
      .goods-price {
        font-weight: bold;
        color: red;
        font-size: 13px;
      }
    }
  }
}
</style>
