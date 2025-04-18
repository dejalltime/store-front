<template>
  <div class="shopping-cart" v-if="hasCartItems">
    <table class="shopping-cart-table">
      <thead>
        <tr>
          <th>Item</th>
          <th>Quantity</th>
          <th>Price</th>
          <th>Total</th>
          <th></th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in cartItems" :key="item.product.id">
          <td>{{ item.product.name }}</td>
          <td>{{ item.quantity }}</td>
          <td>{{ item.product.price }}</td>
          <td>{{ getItemTotal(item) }}</td>
          <td><button @click="removeFromCart(item)">Remove</button></td>
        </tr>
      </tbody>
    </table>
    <button class="checkout-button" @click="submitOrder">Checkout</button>
  </div>
  <div class="shopping-cart" v-else>
    <h3>Your shopping cart is empty</h3>
  </div>
</template>

<script>
export default {
  name: 'ShoppingCart',
  props: ['cartItems'],
  computed: {
    hasCartItems() {
      return this.cartItems.length > 0
    },
  },
  methods: {
    getItemTotal(item) {
      const quantity = item.quantity
      const price = item.product.price
      const total = quantity * price
      return total.toFixed(2)
    },
    removeFromCart(item) {
      const index = this.cartItems.indexOf(item)
      if (index > -1) {
        this.$emit('removeFromCart', index)
      }
    },
    submitOrder() {
      this.$emit('submitOrder')
    }
  }
}
</script>

<style scoped>
.shopping-cart {
  background-color: #ffffff;
  margin: 2rem auto;
  padding: 2rem;
  max-width: 900px;
  border-radius: 8px;
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.05);
  font-family: 'Segoe UI', sans-serif;
}

.shopping-cart h3 {
  text-align: center;
  color: #444;
  font-weight: 500;
  font-size: 1.2rem;
}

.shopping-cart-table {
  width: 100%;
  border-collapse: collapse;
  margin-bottom: 2rem;
}

.shopping-cart-table th {
  text-align: left;
  background-color: #001e73;
  color: white;
  padding: 1rem;
  font-size: 1rem;
}

.shopping-cart-table td {
  padding: 1rem;
  border-bottom: 1px solid #e0e0e0;
  font-size: 0.95rem;
}

.shopping-cart-table td:last-child {
  text-align: right;
}

.shopping-cart-table td button {
  background-color: transparent;
  border: none;
  color: #d32f2f;
  cursor: pointer;
  font-weight: bold;
  transition: color 0.2s;
}

.shopping-cart-table td button:hover {
  color: #ff5252;
}

.checkout-button {
  display: block;
  margin-left: auto;
  padding: 0.75rem 1.5rem;
  font-size: 1rem;
  background-color: #001e73;
  color: white;
  border: none;
  border-radius: 4px;
  font-weight: 600;
  cursor: pointer;
  transition: background-color 0.2s ease-in-out;
}

.checkout-button:hover {
  background-color: #ffea00;
  color: #001e73;
}

</style>
