<template>
  <div>
    <div class="product">
      <div class="product-image">
        <img :src="image" />
      </div>
      <div class="product-info">
        <h1>{{ title }}</h1>
        <p v-if="inStock">In Stock</p>
        <p v-else>Out of Stock</p>
        <p v-show="inventory <= 10 && inventory > 0">Almost</p>     
        <span v-if="onSale">On sale</span> 
        <p>Shipping: {{shipping}}</p>
        <ul>
          <li v-for="(detail, index) in details" :key="index">{{detail}}</li>
        </ul>
        <div v-for="(variant, index) in variants" 
          :key="variant.variantId"
          class="color-box"
          :style="{backgroundColor: variant.variantColor}"
         @mouseover="updateProduct(index)"
        />
        <button 
          @click="addToCart" 
          :disabled="!inStock" 
          :class="{disabledButton: !inStock}"
        >
          Add to Cart
        </button>

      </div>   
        <Tabs :reviews="reviews"/>
      <div>
      </div>          
    </div>
  </div>
</template>

<script>
import image1 from "../assets/vmSocks-green-onWhite.jpg"
import image2 from "../assets/vmSocks-blue-onWhite.jpg"
import Tabs from './Tabs.vue'

export default {
  name: 'Socks',
    components: {
    Tabs
    },
        
  props: {
    premium: {
      type: Boolean,
      required: true
    }
  },
  data() {
    return {
      brand: "Vue Mastery",
      product: "Socks",
      selectedVariant: 0,
      inventory: 100,
      onSale: true,
      details: ["80% cotton", "20% polyester", "Gender-neutral" ],
      variants: [
        {
          variantId: 2234,
          variantColor: 'green',
          variantImage: image1,
          variantQuantity: 10
        },
        {
          variantId: 2235,
          variantColor: 'blue',
          variantImage: image2,
          variantQuantity: 0
        } 
      ],
      reviews: []
      }
  },
  methods: {
    addToCart() {
      this.$emit('add-to-cart', this.variants[this.selectedVariant].variantId)
    },
    updateProduct(index) {
      this.selectedVariant = index
    },
    addReviw(productReview) {
      this.reviews.push(productReview)
    }
  },
  computed: {
    title() {
      return `${this.brand} ${this.product}`
    },
    image() {
      return this.variants[this.selectedVariant].variantImage
    },
    inStock() {
      return this.variants[this.selectedVariant].variantQuantity
    },
    shipping() {
      if (this.premium) {
        return "free"
      }
      return 2.99
    }
  }
}
</script>

<style scoped>
</style>
