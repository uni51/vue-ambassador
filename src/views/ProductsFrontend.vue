<template>
  <Products :products="products" :filters="filters" @self-filters="load($event)"/>
</template>

<script lang="ts">
import Products from "@/views/Products.vue";
import {onMounted, reactive, ref} from "vue";
import {Product} from "@/models/product";
import axios from "axios";
import {Filter} from "@/models/filter";

export default {
  name: "ProductsFrontend",
  components: {Products},
  setup() {
    const products = ref<Product[]>([]);
    const filters = reactive({
      s: ''
    });

    onMounted( async () => {
      const {data} = await axios.get('products/frontend');

      products.value = data;
    });

    return {
      products,
      filters
    }
  }
}
</script>
