<template>
  <div class="cart">
    <div class="cart__items">
      <CartItem :array="items" />
    </div>
    <div class="cart__total">
      <h3>Subtotal: {{ totalPrice }}</h3>
      <h3>Discount: ${{ discount }}</h3>
      <h2>Total ${{ absTotal }}</h2>
    </div>
    <!-- <pre>{{ items | json }}</pre> -->
  </div>
</template>

<script>
import CartItem from "./CartItem";
import json from "../../public/cart.json";

export default {
  components: { CartItem },
  data: function () {
    return {
      items: json.items,
      total: "",
    };
  },
  computed: {
    totalPrice: function () {
      let subtotal = 0;
      this.items.forEach((element) => {
        subtotal += element.subtotal;
      });
      return subtotal;
    },
    discount: function () {
      let discount = 0;
      let breakfastArr = [];
      let drinkArr = [];
      this.items.forEach((element) => {
        if (element.category === "breakfast") {
          breakfastArr.push(element);
          if (breakfastArr.length >= 2) {
            discount = this.totalPrice * 0.2;
          }
        } else if (element.category === "drink") {
          drinkArr.push(element);
          if (breakfastArr.length === 1 && drinkArr.length === 1) {
            discount = this.totalPrice * 0.1;
          }
        }
      });
      return discount;
    },
    absTotal: function () {
      let abstotal = this.totalPrice - this.discount;
      return abstotal;
    },
  },
  methods: {},
};
</script>

<style scoped>
.cart {
  display: block;
}
.cart__items {
  border-right: 1px solid #cccccc;
  width: 400px;
}
</style>