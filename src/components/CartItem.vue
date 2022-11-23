<template>
  <div class="cart-item">
    <div class="cart-item-container" v-for="(item, index) in items">
      <h2 class="cart-item__title">{{ item.title }}</h2>
      <div class="cart-item__price">
        <input
          class="cart-item__quantity"
          type="number"
          v-model="item.quantity"
          @change="getSubtotal($event)"
        />
        x {{ item.price }}
        <div class="cart-item__subtotal">
          {{ (item.subtotal = item.quantity * item.price) }}
        </div>
      </div>
      <p>
        <button class="cart-item__button" @click="removeItem(index)">
          Remove from cart
        </button>
      </p>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    array: Array,
  },
  data: function () {
    return {
      items: this.array,
      subtotal: this.total,
    };
  },
  mounted() {},
  methods: {
    removeItem: function (index) {
      this.$delete(this.items, index);
    },
    getSubtotal: function (event) {
      this.subtotal = event.target.value;
    },
    getTotal: function (item) {
      return item.subtotal;
    },
  },
};
</script>

<style scoped>
h2 {
  font-size: 16px;
  text-align: left;
}
.cart-item {
  padding: 20px;
  border-bottom: 1px solid #cccccc;
}
.cart-item:last-child {
  border-bottom: none;
}
.cart-item__price {
  display: flex;
  align-items: flex-start;
  justify-content: flex-start;
}
.cart-item__quantity {
  margin-right: 10px;
  width: 30px;
}
.cart-item__subtotal {
  font-weight: bold;
  text-align: right;
  margin-left: auto;
}
.cart-item__info {
  min-width: 100px;
  width: 75%;
}
</style>