<template>
  <br />
  <div class="product-detail" v-if="productExists">
    <div class="product-image">
      <img :src="product.image" :alt="product.name" />
    </div>
    <div class="product-info">
      <h2>{{ product.name }}</h2>
      <small class="product-id">Product ID: {{ product.id }}</small>
      <p class="description">{{ product.description }}</p>
      <div class="product-controls">
        <p class="price-label">
          <b>Price: <span class="price">${{ product.price.toFixed(2) }}</span></b>
        </p>
        <div class="action-row">
          <input type="number" v-model="quantity" min="1" class="quantity-input" />
          <button @click="addToCart" class="add-button">Add to Cart</button>
        </div>
      </div>
    </div>
  </div>

  <div class="product-detail" v-else>
    <img src="../assets/404.jpg" alt="Product not found" />
    <h3>Oops! That product was not found...</h3>
  </div>
</template>

<script>
export default {
  name: 'ProductDetail',
  props: ['products'],
  data() {
    return {
      quantity: 1
    }
  },
  computed: {
    product() {
      return this.products.find(product => product.id == this.$route.params.id)
    },
    productExists() {
      return !!this.product
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
.product-detail {
  display: flex;
  align-items: flex-start;
  justify-content: center;
  gap: 2rem;
  padding: 2rem;
  background-color: #f8f9fa;
  border-radius: 8px;
  box-shadow: 0 4px 12px rgba(0, 0, 0, 0.05);
}

.product-image {
  flex: 1;
  max-width: 400px;
}

.product-image img {
  width: 100%;
  height: auto;
  border-radius: 8px;
  object-fit: contain;
}

.product-info {
  flex: 1;
  max-width: 500px;
}

.product-info h2 {
  font-size: 1.8rem;
  font-weight: bold;
  color: #001e73; /* Best Buy Blue */
  margin-bottom: 0.5rem;
}

.product-id {
  font-size: 0.9rem;
  color: #666;
  display: block;
  margin-bottom: 1rem;
}

.description {
  font-size: 1rem;
  margin-bottom: 1.5rem;
  line-height: 1.5;
  color: #333;
}

.product-controls {
  display: flex;
  flex-direction: column;
}

.price-label {
  font-size: 1.2rem;
  margin-bottom: 1rem;
}

.price {
  color: #000;
}

.action-row {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.quantity-input {
  width: 60px;
  padding: 0.4rem;
  font-size: 1rem;
  border: 1px solid #ccc;
  border-radius: 4px;
}

.add-button {
  background-color: #ffd500; /* Best Buy Yellow */
  color: #000;
  border: none;
  padding: 0.6rem 1.2rem;
  font-weight: bold;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.2s ease-in-out;
}

.add-button:hover {
  background-color: #f0c400;
}

@media (max-width: 768px) {
  .product-detail {
    flex-direction: column;
    padding: 1rem;
  }

  .product-image, .product-info {
    max-width: 100%;
  }
}
</style>
