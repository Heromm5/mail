<template>
  <div class="bottom-bar">
    <div class="check-content">
      <check-button class="check-button"></check-button>
      <span>全选</span>
    </div>
    <div class="price">合计：{{totalPrice}}</div>
    <div class="calculate">结算({{checkLength}})</div>
  </div>
</template>

<script>
import CheckButton from "components/content/checkButton/CheckButton";

export default {
  components: {
    CheckButton
  },
  computed: {
    totalPrice() {
      return (
        "￥" +
        this.$store.state.cartList
          .filter(item => {
            return item.checked;
          })
          .reduce((preValue, item) => {
            return preValue + item.newPrice * item.count;
          }, 0)
          .toFixed(2)
      );
    },
    checkLength() {
      return this.$store.state.cartList.filter(item => item.checked).length;
    }
  }
};
</script>

<style scoped>
.bottom-bar {
  height: 40px;
  line-height: 40px;
  background-color: #eee;
  position: relative;
  display: flex;
}

.check-content {
  display: flex;
  align-items: center;
  margin-left: 10px;
  width: 60px;
}

.check-button {
  width: 22px;
  height: 20px;
  line-height: 20px;
  margin-right: 5px;
}

.price {
  margin-left: 30px;
  flex: 1;
}

.calculate {
  background-color: orangered;
  color: #fff;
  width: 100px;
  text-align: center;
}
</style>