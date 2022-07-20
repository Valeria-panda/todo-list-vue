<template>
  <ProductsList :products="products" />
  <StandartPagination v-model:page="page" :count="countProducts" :perPage="productsPerPage" />
</template>

<script>
import ProductsList from './components/ProductsList.vue';
import StandartPagination from './components/StandartPagination.vue';
import products from './data/products';

export default {
  name: 'App',
  components: {
    ProductsList,
    StandartPagination
  },
  data() {
    return {
      page: 1,
      productsPerPage: 3,
    }
  },
  computed: {
    products() {
      const offset = (this.page - 1) * this.productsPerPage;
      return products.slice(offset, offset + this.productsPerPage);
    },
    countProducts() {
      return products.length;
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
