<template>
  <div>
    <div class="nav-bar"></div>
    <div class="product">
      <div class="product-image">
        <img :src="image" />
      </div>
      <div class="product-info">
        <h1>{{ product }}</h1>
        <p v-if="inventory > 10">In Stock</p>
        <p v-else>Out of Stock</p>
        <p v-show="inventory <= 10 && inventory > 0">Almost</p>     
        <span v-if="onSale">On sale</span> 
        <ul>
          <li v-for="(detail, index) in details" :key="index">{{detail}}</li>
        </ul>
        <div v-for="variant in variants" 
          :key="variant.variantId"
          class="color-box"
          :style="{backgroundColor: variant.variantColor}"
          @mouseover="updateProduct(variant.variantImage)"
        />
        <button @click="addToCart" 
        :disabled="!inStock" 
        :class="{disabledButton: !inStock}"
        >Add to Cart</button>
        <div class="cart">
          <p>Cart({{cart}})</p>
        </div>
      </div>   
    </div>
  </div>
</template>

<script>
import image1 from "../assets/vmSocks-green-onWhite.jpg"
import image2 from "../assets/vmSocks-blue-onWhite.jpg"

export default {
  name: 'Socks',
  data() {
    return {
      product: "Socks",
      image: image1,
      inventory: 100,
      onSale: true,
      inStock: true,
      details: ["80% cotton", "20% polyester", "Gender-neutral" ],
      cart: 0,
      variants: [
        {
          variantId: 2234,
          variantColor: 'green',
          variantImage: image1
        },
        {
          variantId: 2235,
          variantColor: 'blue',
          variantImage: image2
        } 
      ]
      }
  },
  methods: {
    addToCart() {
      this.cart++
    },
    updateProduct(variantImage) {
      this.image = variantImage
    }
  }
}
</script>

<style scoped>
</style>
