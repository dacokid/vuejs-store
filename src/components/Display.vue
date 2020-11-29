<template>
  <div class="display">
    <Item
      @add="handleAddedProduct"
      @remove="handleRemovedProduct"
      :imgSrc="products[0].imgSrc"
      :id="products[0].id"
      :name="products[0].name"
      :price="products[0].price"
    />
    <Item
      @add="handleAddedProduct"
      @remove="handleRemovedProduct"
      :imgSrc="products[1].imgSrc"
      :id="products[1].id"
      :name="products[1].name"
      :price="products[1].price"
    />
    <Item
      @add="handleAddedProduct"
      @remove="handleRemovedProduct"
      :imgSrc="products[2].imgSrc"
      :id="products[2].id"
      :name="products[2].name"
      :price="products[2].price"
    />

    <b-table sticky-header :data="items" :columns="columns"></b-table>
    <div class="order__cost">
      Total Cost: <br />
      <span>
        $ <strong>{{ total }} </strong></span
      >
      <b-button @click="submitOrder" class="order__button" type="is-success"
        >Checkout</b-button
      >
    </div>
  </div>
</template>

<script>
import Item from "./Item";
import { products } from "../data/mocked-data";
export default {
  components: {
    Item
  },
  data: () => ({
    products,
    total: 0,
    items: [],
    columns: [
      {
        field: "id",
        label: "ID",
        width: 40,
        numeric: true,
        centered: true
      },
      {
        field: "name",
        label: "Product name",
        centered: true
      },
      {
        field: "price",
        label: "Price",
        centered: true
      }
    ]
  }),
  methods: {
    handleAddedProduct(product) {
      this.items.push(product);
      this.handleTotalCost();
    },
    handleRemovedProduct(id) {
      const found = this.items.find(product => product.id === id);
      if (found) {
        this.items.pop(found);
        this.handleTotalCost();
      }
    },
    handleTotalCost() {
      this.total = 0;
      this.items.map(item => {
        this.total = this.total + item.price;
      });

      let filtered = this.items.filter(this.handleDiscount);

      if (filtered.length > 1) {
        this.total = this.total - this.total * 0.1;
      }

      console.log(this.total);
    },
    handleDiscount(item) {
      return item.id === 1;
    },
    submitOrder() {
      alert(
        `Final Order: ${this.items.map(
          item => `${item.name}: $${item.price}`
        )}. Total: ${this.total}`
      );
      console.log(
        `Final Order: ${this.items.map(
          item => `${item.name}: $${item.price}`
        )}. Total: ${this.total}`
      );
    }
  }
};
</script>

<style>
.display {
  display: flex;
  margin: 0 auto;
  padding: 50px 50px 0;
  justify-content: center;
  width: 100vw;
}

.b-table {
  padding: 16px;
  margin: 30px;
  display: flex;
  flex-direction: column;
  background: rgb(255, 255, 255);
  border: 1px solid rgba(200, 200, 200, 0.9);
  border-radius: 5px;
  box-shadow: 1px 1px 3px rgba(0, 0, 0, 0.5);
  min-width: 400px;
}

.order__cost {
  width: 200px;
  height: 200px;
  border: 1px solid rgba(200, 200, 200, 0.9);
  border-radius: 5px;
  box-shadow: 1px 1px 3px rgba(0, 0, 0, 0.5);
  padding: 16px;
  margin: 30px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}

.order__cost > span {
  color: green;
  font-weight: 500;
}

.order__cost strong {
  color: blueviolet;
  font-weight: 500;
  font-size: 1.4em;
}
</style>
