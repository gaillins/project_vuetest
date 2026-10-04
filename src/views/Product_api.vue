<template>
  <div class="container my-5">
    <div class="row">
      <div class="col-md-4 mb-4" v-for="product in products" :key="product.id">
        <div class="card h-100">
          <img
            :src="product.thumbnail"
            class="card-img-top"
            alt="Product Image"
            style="object-fit: contain; width: 100%; height: 200px"
          />

          <div class="card-body">
            <h5 class="card-title">{{ product.title }}</h5>
          </div>

          <div class="card-footer">
            <small class="text-muted"> Price: ${{ product.price }} </small>

            <button
              type="button"
              class="btn btn-outline-primary float-end"
              @click="addToCart(product)"
            >
              Add
            </button>
          </div>
        </div>
      </div>
    </div>

    <!-- แสดงจำนวนสินค้าในตะกร้า -->
    <div class="mt-4">
      <h4>Cart: {{ cart.length }} items</h4>
    </div>
  </div>
</template>

<script>
import { ref, onMounted } from "vue";

export default {
  setup() {
    const products = ref([]);
    const cart = ref([]);

    const fetchProducts = async () => {
      try {
        const response = await fetch("https://dummyjson.com/products");
        const data = await response.json();

        products.value = data.products;
      } catch (error) {
        console.error("Error fetching products:", error);
      }
    };

    const addToCart = (product) => {
      cart.value.push(product);
    };

    onMounted(fetchProducts);

    return {
      products,
      cart,
      addToCart,
    };
  },
};
</script>
