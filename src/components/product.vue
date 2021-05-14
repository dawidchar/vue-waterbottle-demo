<template>
  <div class="product_page">
    <div class="product_image">
      <img :src="image" />
    </div>

    <div class="product_info">
      <h1>{{ productTitle }}</h1>
      <p v-if="inStock">In Stock</p>
      <p v-else><i>Out of Stock</i></p>
      <p>Shipping: {{ shipping }}</p>

      <ul>
        <li v-for="detail in details" v-bind:key="detail">{{ detail }}</li>
      </ul>

      <div class="color_box_container">
        <div
          class="color_box"
          v-for="(variant, index) in variants"
          :key="variant.variantId"
          :style="{ backgroundColor: variant.variantColor }"
          @mouseover="updateProduct(index)"
        ></div>
      </div>

      <button
        v-on:click="addToCart"
        :disabled="!inStock"
        class="addToCart"
        :class="{ disabledButton: !inStock }"
      >
        Add to cart
      </button>
    </div>
  </div>
</template>

<script>
export default {
  name: "product",
  props: ['premium'],
  data() {
    return {
      product: "Water Bottle",
      selectedVariant: 0,
      details: ["Stainless Steel", "1L Capacity", "Awesome🤘"],
      variants: [
        {
          variantId: 2234,
          variantColor: "Green",
          variantImage: require("../assets/bottle-green.jpg"),
          variantQuantity: 10,
        },
        {
          variantId: 2235,
          variantColor: "Red",
          variantImage: require("../assets/bottle-red.jpg"),
          variantQuantity: 1,
        },
        {
          variantId: 2236,
          variantColor: "Blue",
          variantImage: require("../assets/bottle-blue.jpg"),
          variantQuantity: 0,
        },
      ],
    };
  },
  methods: {
    addToCart() {
      this.$emit("add-to-cart", this.variants[this.selectedVariant].variantId);
    },
    updateProduct(index) {
      this.selectedVariant = index;
    }
  },
  computed: {
    productTitle() {
      return `${this.product} - ${
        this.variants[this.selectedVariant].variantColor
      }`;
    },
    image() {
      return this.variants[this.selectedVariant].variantImage;
    },
    inStock() {
      return this.variants[this.selectedVariant].variantQuantity > 0;
    },
    shipping() {
      if (this.premium) {
        return "Free⭐";
      }
      return 2.99;
    },
  },
};
</script>