<template>
  <b-navbar>
    <template slot="brand">
      <b-navbar-item tag="router-link" :to="{ path: '/' }">
        <h1>Store</h1>
      </b-navbar-item>
    </template>
    <template slot="start">
      <b-navbar-item href="#">
        Home
      </b-navbar-item>
      <b-navbar-item @click="getProducts" href="#">
        Show products
      </b-navbar-item>
    </template>
  </b-navbar>
</template>

<script>
import { products } from "../data/mocked-data";
export default {
  data: () => ({
    products
  }),
  methods: {
    getProducts() {
      alert(
        `Products: ${this.products.map(
          product =>
            `${product.name}: ${product.price}, weights ${product.weight}.`
        )}`
      );
    }
  }
};
</script>
<style>
.navbar {
  background: #5b14e0;
  box-shadow: 0 1px 3px rgba(0, 0, 0, 0.5);
  position: sticky;
  width: 100%;
  z-index: 1;
}

.navbar-item {
  color: #fff;
}

h1 {
  color: orangered;
  font-size: 16px;
}

.cart {
  display: flex;
}
</style>
