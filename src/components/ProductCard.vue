<template>
  <div class="product-card">
    <img :src="product.image" alt="Product Image" class="product-image" />
    <router-link :to="`/product/${product.id}`">
      <h2 class="product-title">{{ product.name }}</h2>
    </router-link>
    <p class="product-description">{{ product.description }}</p>
    <div class="product-details">
      <div class="product-price">
        <p class="price">${{ product.price.toFixed(2) }}</p>
      </div>
      <div class="product-controls">
        <input type="number" v-model="quantity" min="1" class="quantity-input" />
        <button @click="addToCart" class="add-button">Add to Cart</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'ProductCard',
  props: ['product'],
  data() {
    return {
      quantity: 1
    }
  },
  methods: {
    addToCart() {
      this.$emit('addToCart', {
        productId: this.product.id,
        quantity: this.quantity
      })
    }
  }
}
</script>

<style scoped>
.product-card {
  background-color: #fff;
  border: 1px solid #e0e0e0;
  border-radius: 8px;
  padding: 1rem;
  box-shadow: 0 4px 8px rgba(0,0,0,0.05);
  transition: box-shadow 0.2s ease-in-out;
  width: 100%;
  max-width: 300px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.product-card:hover {
  box-shadow: 0 6px 16px rgba(0,0,0,0.1);
}

.product-image {
  width: 100%;
  height: 180px;
  object-fit: contain;
  margin-bottom: 0.75rem;
}

.product-title {
  font-size: 1.1rem;
  font-weight: 700;
  color: #001e73; /* BestBuy Blue */
  margin-bottom: 0.25rem;
  text-decoration: none;
}

.product-title:hover {
  text-decoration: underline;
}

.product-description {
  font-size: 0.9rem;
  color: #444;
  margin-bottom: 0.5rem;
}

.product-details {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-top: auto;
}

.product-price .price {
  font-size: 1.2rem;
  font-weight: bold;
  color: #000;
}

.product-controls {
  display: flex;
  align-items: center;
  gap: 0.5rem;
}

.quantity-input {
  width: 50px;
  padding: 0.25rem;
  font-size: 0.9rem;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.add-button {
  background-color: #ffd500; /* BestBuy Yellow */
  color: #000;
  border: none;
  padding: 0.4rem 0.75rem;
  border-radius: 4px;
  font-weight: 600;
  cursor: pointer;
  transition: background-color 0.2s ease;
}

.add-button:hover {
  background-color: #f0c400;
}
</style>
