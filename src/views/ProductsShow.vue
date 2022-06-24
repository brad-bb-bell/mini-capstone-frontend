<script>
import axios from "axios";

export default {
  data: function () {
    return {
      product: {},
      currentSupplier: {},
      editProduct: {},
    };
  },
  created: function () {
    axios.get("/products/" + this.$route.params.id + ".json").then((response) => {
      this.product = response.data;
      console.log(response.data);
    });
  },
  methods: {
    showSupplier: function (supplier) {
      console.log("supplier: ", supplier);
      this.currentSupplier = supplier;
      document.querySelector("#product-supplier").showModal();
    },
    showProduct: function (product) {
      console.log(product);
      this.editProduct = product;
      document.querySelector("#product-update").showModal();
    },
    updateProduct: function () {
      console.log("Update action for:", this.editProduct);
      axios
        .patch("/products/" + this.editProduct.id + ".json", this.editProduct)
        .then((response) => {
          console.log("Success", response.data);
        })
        .catch((error) => console.log(error.response));
    },
    destroyProduct: function () {
      console.log("Destroying...", this.editProduct.name);
      axios.delete("/products/" + this.editProduct.id + ".json").then((response) => {
        console.log("Success,", response.data);
      });
      this.$router.push("/products");
    },
  },
};
</script>

<template>
  <div class="products-show">
    <h3>{{ product.name }}</h3>
    <p>{{ product.description }}</p>
    <p>Price: ${{ product.price }}</p>
    <p>Quantity: {{ product.quantity }}</p>
    <p>
      Supplier:
      <button v-on:click="showSupplier(product.supplier)">{{ product.supplier.name }}</button>
    </p>
    <p><img v-bind:src="product.images[0]?.url" v-bind:key="product.id" /></p>
    <p><button v-on:click="showProduct(product)">Edit/Delete</button></p>
  </div>

  <dialog id="product-supplier">
    <form method="dialog">
      <h1>{{ currentSupplier.name }}</h1>
      <p>Email: {{ currentSupplier.email }}</p>
      <p>Phone number: {{ currentSupplier.phone_number }}</p>
      <p><button>Close</button></p>
    </form>
  </dialog>
  <dialog id="product-update">
    <form method="dialog">
      <p>
        Name:
        <input type="text" v-model="editProduct.name" />
      </p>
      <p>
        Description:
        <input type="text" v-model="editProduct.description" />
      </p>
      <p>
        Price:
        <input type="text" v-model="editProduct.price" />
      </p>
      <p>
        Quanity:
        <input type="text" v-model="editProduct.quantity" />
      </p>
      <button v-on:click="updateProduct()">Save Updated Info</button>
      <button v-on:click="destroyProduct()">Delete Product</button>
      <button v-on:click="closeWindow()">Close</button>
    </form>
  </dialog>
</template>

<style></style>
