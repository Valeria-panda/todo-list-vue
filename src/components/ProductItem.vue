<template>
    <li class="catalog__item">
        <a class="catalog__pic" href="#">
            <img :src="product.image" :alt="product.title">
        </a>
        <h3 class="catalog__title">
            <a href="#">
                {{ product.title }}
            </a>
        </h3>
        <span class="catalog__price">
            {{ product.price }} ₽
        </span>
        <ul class="colors colors--black">
            <li class="colors__item" v-for="(color, index) in product.colorValues" :key="index">
                <label class="colors__label">
                    <input class="colors__radio sr-only" type="radio" :value="color">
                    <span class="colors__value" :style="'background-color:' + color">
                    </span>
                </label>
            </li>
        </ul>
    </li>
</template>
<script>

export default {
    name: 'ProductItem',
    props: {
        product: {
            required: true,
            type: Object
        }
    },

}
</script>
<style>
.catalog__item {
    background-color: #fff;
}
</style>