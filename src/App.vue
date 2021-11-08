<template>

<header class="top-bar spread">
    <nav class="top-bar-nav">
      <router-link to="/" class="top-bar-link">
        <i class="icofont-spoon-and-fork"></i>
        <span>Home</span>
      </router-link>
      <router-link to="/products" class="top-bar-link">
        <span>Products</span>
      </router-link>

      <router-link to="/past-orders" class="top-bar-link">
        <span>Past Orders</span>
      </router-link>
    </nav>

    <div @click="toggleSidebar" class="top-bar-cart-link">
      <i class="icofont-cart-alt icofont-1x"></i>
      <span>Cart ({{ totalQuantity() }})</span>
    </div>
  </header>

  <router-view :inventory="inventory" :addToCart="addToCart" />

  <Sidebar
    v-if="showSidebar"
    :toggle="toggleSidebar"
    :cart="cart"
    :inventory="inventory"
    :remove="removeItemFromCart"
  />
</template>

<script>
import Sidebar from './components/Sidebar'
import food from './food.json'

export default {
  components: {
    Sidebar
  },
  data () {
    return {
      showSidebar: false,
      cart: {},
      inventory: food
    }
  },
  methods: {
    totalQuantity () {
      return Object.values(this.cart).reduce((acc, curr) => {
        return acc + curr
      }, 0)
    },

    addToCart (name, quantity) {
      if (!this.cart[name]) {
        this.cart[name] = 0
      }
      this.cart[name] += quantity
    },

    removeItemFromCart (name) {
      delete this.cart[name]
    },

    toggleSidebar () {
      this.showSidebar = !this.showSidebar
    }
  }
}
</script>
