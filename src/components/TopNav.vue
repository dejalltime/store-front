<template>
  <nav>
    <div class="logo">
      <a href="/">
        <img src="../assets/bestbuy.png" alt="BestBuy Logo" />
      </a>
    </div>
    <button class="hamburger" @click="toggleNav">
      <span class="hamburger-icon"></span>
    </button>
    <ul class="nav-links" :class="{ 'nav-links--open': isNavOpen }">
      <li><router-link to="/" @click="closeNav">Products</router-link></li>
      <li><router-link to="/cart" @click="closeNav">Cart ({{ cartItemCount }})</router-link></li>
    </ul>
  </nav>
</template>

<script>
export default {
  name: 'TopNav',
  props: ['cartItemCount'],
  data() {
    return {
      isNavOpen: false
    }
  },
  methods: {
    toggleNav() {
      this.isNavOpen = !this.isNavOpen
    },
    closeNav() {
      this.isNavOpen = false
    }
  }
}
</script>

<style scoped>
nav {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background-color: #001e73;
  color: white;
  padding: 0.5rem 1rem;
  position: fixed;
  top: 0;
  left: 0;
  right: 0;
  height: 64px;
  z-index: 1000;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
  font-family: 'Segoe UI', sans-serif;
}

nav img {
  width: 48px;
  height: auto;
}

.nav-links {
  display: flex;
  list-style: none;
  font-size: 1rem;
  font-weight: 600;
}

.nav-links li {
  margin-left: 1.5rem;
}

.nav-links a {
  color: white;
  text-decoration: none;
  transition: color 0.2s ease-in-out;
}

.nav-links a:hover {
  color: #ffea00; /* BestBuy yellow */
}

.hamburger {
  display: none;
  background: none;
  border: none;
  cursor: pointer;
}

.hamburger-icon {
  width: 24px;
  height: 2px;
  background-color: white;
  position: relative;
  display: block;
}

.hamburger-icon::before,
.hamburger-icon::after {
  content: '';
  width: 24px;
  height: 2px;
  background-color: white;
  position: absolute;
  left: 0;
}

.hamburger-icon::before {
  top: -6px;
}

.hamburger-icon::after {
  top: 6px;
}

@media (max-width: 768px) {
  .nav-links {
    display: none;
    position: absolute;
    top: 64px;
    left: 0;
    right: 0;
    background-color: #001e73;
    padding: 1rem;
    flex-direction: column;
    align-items: flex-start;
  }

  .nav-links--open {
    display: flex;
  }

  .nav-links--open li {
    padding: 0.5rem 0;
  }

  .hamburger {
    display: block;
  }
}
</style>
