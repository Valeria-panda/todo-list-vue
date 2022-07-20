<template>
    <section class="catalog">
        <ul class="catalog__list">
            <ProductItem v-for='(product, index) in products' :product='product' :key='index' />
        </ul>
    </section>
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