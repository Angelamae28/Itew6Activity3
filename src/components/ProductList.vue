<template>
  <div>
    <h2 class="center">Products</h2>
    <div class="product-columns">
      <div v-for="(column, index) in productColumns" :key="index" class="product-column">
        <ul class="product-list">
          <li v-for="product in column" :key="product.id" class="product-item">
            <div>{{ product.name }}</div>
            <div>₱{{ product.price }}</div>
            <button class="add-to-cart-btn" @click="addToCart(product)">Add to Cart</button>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    products: {
      type: Array,
      required: true,
    },
  },
  data() {
    return {
      productColumns: [], 
    };
  },
  mounted() {
    this.splitProductsIntoColumns();
  },
  methods: {
    addToCart(product) {
      this.$emit("add-to-cart", product);
    },
    splitProductsIntoColumns() {
      const productsCopy = [...this.products];
      const numColumns = 2;
      const productsPerColumn = Math.ceil(this.products.length / numColumns);
      for (let i = 0; i < numColumns; i++) {
        this.productColumns.push(productsCopy.splice(0, productsPerColumn));
      }
    }
  }
}
</script>
