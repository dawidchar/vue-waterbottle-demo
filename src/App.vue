<template>
  <div id="app">
    <div class="cart">
      <p>Cart({{ cart.length }})</p>
    </div>
    <product @add-to-cart="updateCart" :premium="false"></product>
    <product @add-to-cart="updateCart" :premium="true"></product>
  </div>
</template>

<script>
import product from "./components/product";
export default {
  name: "App",
  data: () => ({
    cart: [],
  }),
  components: { product },
  methods: {
    updateCart(id) {
      this.cart.push(id);
    },
  },
};
</script>

<style>
@import "./assets/style.css";
</style>
