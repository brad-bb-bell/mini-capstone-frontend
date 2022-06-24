<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newProduct: {},
    };
  },
  created: function () {},
  methods: {
    createProduct: function () {
      axios.post("/products.json", this.newProduct).then((response) => {
        console.log("Success!", response.data);
        this.$router.push("/products");
      });
    },
  },
};
</script>

<template>
  <h1>Create new product</h1>
  <p>
    Name:
    <input type="text" v-model="newProduct.name" />
  </p>
  <p>
    Description:
    <input type="text" v-model="newProduct.description" />
  </p>
  <p>
    Price:
    <input type="text" v-model="newProduct.price" />
  </p>
  <p>
    Supplier_ID:
    <input type="text" v-model="newProduct.supplier_id" />
  </p>
  <button v-on:click="createProduct()">Create</button>
</template>

<style></style>
