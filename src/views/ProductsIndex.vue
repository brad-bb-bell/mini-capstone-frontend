<script>
import axios from "axios";

export default {
  data: function () {
    return {
      products: [],
    };
  },
  created: function () {
    axios.get("/products.json").then((response) => {
      this.products = response.data;
      console.log(response.data);
    });
  },
  methods: {},
};
</script>

<template>
  <!-- <div class="products-index">
    <div v-for="product in products" v-bind:key="product.id">
      <h3>
        <router-link v-bind:to="`/products/${product.id}`">{{ product.name }}</router-link>
      </h3>
      <p>{{ product.description }}</p>
      <p>${{ product.price }}</p>
      <p>
        <a v-bind:href="`/products/${product.id}`">
          <img v-bind:src="product.images[0]?.url" v-bind:key="product.id" />
        </a>
      </p>
    </div>
  </div> -->

  <div class="card" style="width: 40rem">
    <div class="col">
      <div v-for="product in products" v-bind:key="product.id">
        <img
          v-bind:src="product.images[0]?.url"
          v-bind:key="product.id"
          class="card-img-top"
          v-bind:alt="product.name"
        />
        <div class="card-body">
          <h5 class="card-title">{{ product.name }}</h5>
          <p class="card-text">
            {{ product.description }}
          </p>
          <a v-bind:href="`/products/${product.id}`" class="btn btn-primary">More</a>
        </div>
      </div>
    </div>
  </div>
</template>

<style>
.card {
  margin-bottom: 10px;
}
</style>
