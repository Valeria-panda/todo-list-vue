<template>
  <main class="content container">
    <div class="content__top content__top--catalog">
      <h1 class="content__title">
        Каталог
      </h1>
      <span class="content__info">
        152 товара
      </span>
    </div>

    <div class="content__catalog">
      <ProductsFilter v-model:filter-price-from="filterPriceFrom" v-model:filter-price-to="filterPriceTo"
        v-model:filter-category-id="filterCategoryId" v-model:filter-color-code="filterColorCode" />
      <section class="catalog">
        <ProductsList :products="products" />
      </section>
    </div>
    <StandartPagination v-model:page="page" :count="countProducts" :perPage="productsPerPage" />
  </main>
</template>

<script>
import ProductsList from './components/ProductsList.vue';
import ProductsFilter from './components/ProductsFilter.vue';
import StandartPagination from './components/StandartPagination.vue';
import products from './data/products';

export default {
  name: 'App',
  components: {
    ProductsList,
    ProductsFilter,
    StandartPagination,
  },
  data() {
    return {
      filterPriceFrom: 5000,
      filterPriceTo: 0,
      filterCategoryId: 0,
      filterColorCode: '#73b6ea',
      page: 1,
      productsPerPage: 6,
    }
  },
  computed: {
    filteredProducts() {
      let filteredProducts = products;

      if (this.filterPriceFrom >= 0) {
        filteredProducts = filteredProducts.filter(product => product.price >= this.filterPriceFrom);
      }
      if (this.filterPriceTo > 0) {
        filteredProducts = filteredProducts.filter(product => product.price <= this.filterPriceTo);
      }
      if (this.filterCategoryId) {
        filteredProducts = filteredProducts.filter(product => product.categoryId === this.filterCategoryId);
      }

      return filteredProducts;
    },
    products() {
      const offset = (this.page - 1) * this.productsPerPage;
      return this.filteredProducts.slice(offset, offset + this.productsPerPage);
    },
    countProducts() {
      return products.length;
    }
  },
  watch: {
    filterPriceFrom: function (val) {
      console.log(val);
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
