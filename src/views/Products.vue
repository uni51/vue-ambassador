<template>
  <div class="col-md-12 mb-4 input-group">
    <input class="form-control" placeholder="Search" @keyup="search($event.target.value)"/>
  </div>  

  <div class="row row-cols-1 row-cols-sm-2 row-cols-md-3 g-3">
    <div class="col" v-for="product in products" :key="product.id">
      <div class="card shadow-sm">
        <img :src="product.image" height="200"/>

        <div class="card-body">
          <p class="card-text">{{ product.title }}</p>
          <div class="d-flex justify-content-between align-items-center">
            <small class="text-muted">{{ product.price }}</small>
          </div>
        </div>
      </div>
    </div>
  </div>  
</template>

<script lang="ts">
import {SetupContext} from 'vue';

export default {
  name: "Products",
  props: ['products', 'filters'],
  emits: ['self-filters'],
  setup(props: any, context: SetupContext) {

    const search = (s: string) => {
      context.emit('self-filters', {
        s
      });
    }

    return {
      search
    }
  }
}
</script>
