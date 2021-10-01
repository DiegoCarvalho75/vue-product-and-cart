<template>
  <div class="home">
    <div class="splash-container">
      <div class="splash">
        <h1>Splendid Food!!!!</h1>
      </div>
    </div>
    <div></div>
    <main class="wrapper">
      <h2>
        Recommended
      </h2>
      <div class="recommended">
        <ProductCard
          class="card"
          v-for="(product, index) in inventory.slice(0, 3)"
          :key="product.id"
          :index="index"
          :product="product"
          :addToCart="addToCart"
        >
        </ProductCard>
      </div>
    </main>
  </div>
</template>

<script>
import ProductCard from '../components/ProductCard'

export default {
  name: 'Home',
  props: ['inventory', 'addToCart', 'product'],
  data () {
    return {}
  },
  components: {
    ProductCard
  }
}
</script>
