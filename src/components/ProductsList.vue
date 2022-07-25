<template>
    <ul class="catalog__list">
        <ProductItem v-for='product in products' :product='product' :key='product.id' />
    </ul>
</template>

<script>
import ProductItem from '../components/ProductItem.vue';

export default {
    name: 'ProductsList',
    props: {
        products: {
            type: Number,
            required: true
        },
    },
    components: {
        ProductItem,
    }
}
</script>
<style>
</style>