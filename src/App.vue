<template>
  <div id="app">
    <div>
      <product-list :products="products" @add-to-cart="addToCart"></product-list>
    </div>
    <div>
      <shopping-cart :cart="cart" @remove-from-cart="removeFromCart" @update-quantity="updateQuantity"></shopping-cart>
    </div>
  </div>
</template>

<script>
import ProductList from "./components/ProductList.vue";
import ShoppingCart from "./components/ShoppingCart.vue";

export default {
  name: "App",
  components: {
    ProductList,
    ShoppingCart,
  },
  data() {
    return {
      products: [
        { id: 1, name: "Nike Dunk Low", price: 5500 },
        { id: 2, name: "Adidas Samba", price: 6800 },
        { id: 3, name: "New Balance 550", price: 5800 },
        { id: 4, name: "Converse Chuck Taylor", price: 3400 },
        { id: 5, name: "Vans Authentic", price: 3100 }
      ],
      cart: [],
    };
  },
  methods: {
    addToCart(product) {
      const existingItemIndex = this.cart.findIndex(item => item.id === product.id);
      if (existingItemIndex !== -1) {
        this.cart[existingItemIndex].quantity++;
      } else {
        this.cart.push({ ...product, quantity: 1 });
      }
    },
    removeFromCart(productId) {
      this.cart = this.cart.filter(item => item.id !== productId);
    },
    updateQuantity(payload) {
      const { productId, quantity } = payload;
      const cartItem = this.cart.find(item => item.id === productId);
      if (cartItem) {
        cartItem.quantity = quantity;
      }
    },
  },
};
</script>