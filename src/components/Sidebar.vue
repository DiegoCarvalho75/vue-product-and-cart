<template>
  <aside class="cart-container">
    <div class="cart">
      <h1 class="cart-title spread">
        <span>
          Cart
          <i class="icofont-cart-alt icofont-1x"></i>
        </span>
        <button @click="toggle" class="cart-close">
          &times;
        </button>
      </h1>

      <div class="cart-body">
        <table class="cart-table">
          <thead v-if="Object.keys(cart).length">
            <tr>
              <th>
                <span class="sr-only">Product Image</span>
              </th>
              <th>Product</th>
              <th>Product</th>
              <th>Price</th>
              <th>Qty</th>
              <th>Total</th>
              <th>
                <span class="sr-only">Actions</span>
              </th>
            </tr>
          </thead>
          <tbody>
            <tr
              v-for="(quantity, name) in cart"
              :key="name"
            >
              <td>
                <i
                  class="icofont-{{ name }} icofont-3x"
                ></i>
              </td>
              <td>{{ name }}</td>
              <td>{{ getPrice(name) }}</td>
              <td class="center">{{ quantity }}</td>
              <td>
                $
                {{ (quantity * getPrice(name)).toFixed(2) }}
              </td>
              <td class="center">
                <button
                  @click="remove(name)"
                  class="btn btn-light cart-remove"
                >
                  &times;
                </button>
              </td>
            </tr>
          </tbody>
        </table>
        <p class="center">
          <em
            ><span v-if="!Object.keys(cart).length">
              No items in cart</span
            ></em
          >
        </p>
        <div v-if="Object.keys(cart).length" class="spread">
          <span>
            <strong>Total:</strong> $ {{ calculateTotal() }}
          </span>
          <button class="btn btn-light">Checkout</button>
        </div>
      </div>
    </div>
  </aside>
</template>

<script>
export default {
  name: 'Sidebar',
  props: ['toggle', 'cart', 'inventory', 'remove'],
  methods: {
    getPrice (name) {
      const product = this.inventory.find((p) => {
        return p.name === name
      })
      return product.price.USD.toFixed(2)
    },
    calculateTotal () {
      const total = Object.entries(this.cart).reduce(
        (sum, current, index) => {
          return (
            sum + current[1] * this.getPrice(current[0])
          )
        },
        0
      )
      return total.toFixed(2)
    }
  }
}
</script>
