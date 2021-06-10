<template>
  <Products :products="products" :filters="filters" @set-filters="load"/>
</template>

<script lang="ts">
import Products from "@/views/Products.vue";
import {onMounted, reactive, ref} from "vue";
import {Product} from "@/models/product";
import axios from "axios";
import {Filter} from "@/models/filter";

export default {
  name: "ProductsBackend",
  components: {Products},
  setup() {
    const products = ref<Product[]>([]);
    const filters = reactive({
      s: ''
    });

    const load = async (f: Filter) => {
      filters.s = f.s;
      const arr = [];

      if (filters.s) {
        arr.push(`s=${filters.s}`);
      }

      const {data} = await axios.get(`products/backend?${arr.join('&')}`);

      products.value = data.data;
    };

    onMounted(() => load(filters));

    return {
      products,
      filters,
      load
    }
  }  
}
</script>
