<template>
  <div class="item">
    <img :src="imgSrc" :alt="name" />
    {{ name }}
    <p>
      $<span>{{ price }}</span>
    </p>
    <b-button @click="addToCart">Add to cart</b-button>
    <b-button @click="removeFromCart">Remove from cart</b-button>
  </div>
</template>

<script>
export default {
  props: {
    imgSrc: { type: String },
    id: { type: Number },
    name: { type: String },
    price: { type: Number }
  },
  methods: {
    addToCart() {
      const id = this.id;
      const name = this.name;
      const price = this.price;
      const addedProduct = {
        id,
        name,
        price
      };
      this.$emit("add", addedProduct);
    },
    removeFromCart() {
      const id = this.id;
      this.$emit("remove", id);
    }
  }
};
</script>

<style>
.item {
  padding: 16px;
  margin: 30px;
  display: flex;
  flex-direction: column;
  background: rgb(255, 255, 255);
  border: 1px solid rgba(200, 200, 200, 0.9);
  border-radius: 5px;
  box-shadow: 1px 1px 3px rgba(0, 0, 0, 0.5);
  height: fit-content;
}

.item button {
  margin-top: 12px;
}

img {
  max-height: 150px;
  object-fit: contain;
}

p {
  font-weight: 600;
  color: green;
}

p span {
  font-size: 1.4em;
}
</style>
