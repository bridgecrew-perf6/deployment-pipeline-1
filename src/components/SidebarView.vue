<template>
    <aside class="cart-container">
        <div class="cart">
            <h1 class="cart-title spread">
            <span>
                Cart
                <i class="icofont-cart-alt icofont-1x"></i>
            </span>
            <button @click="toggle" class="cart-close">&times;</button>
            </h1>

            <div class="cart-body">
            <table class="cart-table">
                <thead>
                <tr>
                    <th><span class="sr-only">Product Image</span></th>
                    <th>Product</th>
                    <th>Price</th>
                    <th>Qty</th>
                    <th>Total</th>
                    <th><span class="sr-only">Actions</span></th>
                </tr>
                </thead>
                <tbody>
                <tr v-for="(quantity, key, i) in cart" :key="i">
                    <td><i class="icofont-carrot icofont-3x"></i></td>
                    <td>{{ key }}</td>
                    <td>${{ getPrice(key) }}</td>
                    <td class="center">{{ quantity }}</td>
                    <td>${{ quantity * getPrice(key) }}</td>
                    <td class="center">
                    <button @click="remove(key)" class="btn btn-light cart-remove">
                        &times;
                    </button>
                    </td>
                </tr>
                </tbody>
            </table>

            <p class="center" v-if="!Object.keys(cart).length" ><em>No items in cart</em></p>
            <div class="spread">
                <span><strong>Total:</strong> ${{ calculateTotal() }}</span>
                <button class="btn btn-light">Checkout</button>
            </div>
            </div>
        </div>
    </aside>
</template>

<script>
export default ({
  props: ['toggle', 'cart', 'inventory', 'remove'],
  methods: {
    getPrice (name) {
      const product = this.inventory.find((item) => {
        return item.name === name
      })
      return product.price.USD
    },
    calculateTotal () {
      const total = Object.entries(this.cart).reduce((sum, currentItem, index) => {
        return sum + (currentItem[1] * this.getPrice(currentItem[0]))
      }, 0)
      return total.toFixed(2)
    }
  }
})
</script>
