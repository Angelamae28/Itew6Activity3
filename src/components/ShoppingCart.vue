<template>
  <div class="shopping-cart">
    <h2 class="center">Shopping Cart</h2>
    <div class="cart-items">
      <div v-for="item in cart" :key="item.id" class="cart-item">
        <div class="item-details">
          <div>{{ item.name }}</div>
          <div>₱{{ item.price }}</div>
        </div>
        <div class="item-controls">
          <input type="number" v-model="item.quantity" @change="updateQuantity(item.id, item.quantity)">
          <button class="remove-from-cart-btn" @click="removeFromCart(item.id)">Remove</button>
        </div>
      </div>
    </div>
    <div class="total">Total: ₱{{ totalPrice }}</div>
  </div>
</template>

<script>
export default {
  props: {
    cart: {
      type: Array,
      required: true,
    },
  },
  computed: {
    totalPrice() {
      return this.cart.reduce((total, item) => total + item.price * item.quantity, 0);
    },
  },
  methods: {
    removeFromCart(productId) {
      this.$emit("remove-from-cart", productId);
    },
    updateQuantity(productId, quantity) {
      this.$emit("update-quantity", { productId, quantity: parseInt(quantity) });
    },
  },
};
</script>
