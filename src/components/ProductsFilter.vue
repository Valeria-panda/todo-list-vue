<template>
    <aside class="filter">
        <h2 class="filter__title">Фильтры</h2>
        <form class="filter__form form" action="#" method="get" @submit.prevent="onclickSubmitButton">
            <fieldset class="form__block">
                <legend class="form__legend">Цена</legend>
                <label class="form__label form__label--price">
                    <input class="form__input" type="text" name="min-price" v-model="currentPriceFrom">
                    <span class="form__value">От</span>
                </label>
                <label class="form__label form__label--price">
                    <input class="form__input" type="text" name="max-price" v-model="currentPriceTo">
                    <span class="form__value">До</span>
                </label>
            </fieldset>

            <fieldset class="form__block">
                <legend class="form__legend">Категория</legend>
                <label class="form__label form__label--select">
                    <select class="form__select" type="text" name="category" v-model="currentCategoryId">
                        <option value="0">Все категории</option>
                        <option :value="category.id" v-for="category in categories" :key="category.id">
                            {{ category.title }}
                        </option>
                    </select>
                </label>
            </fieldset>

            <fieldset class="form__block">
                <legend class="form__legend">Цвет</legend>
                <ul class="colors">
                    <li v-for="color in colors" :key="color.id" class="colors__item">
                        <label class="colors__label">
                            <input class="colors__radio sr-only" type="radio" v-model="picked" :value="color.colorCode">
                            <span class="colors__value" :style="'background-color:' + color.colorCode">
                            </span>
                        </label>
                    </li>

                </ul>
            </fieldset>

            <fieldset class="form__block">
                <legend class="form__legend">Объемб в ГБ</legend>
                <ul class="check-list">
                    <li class="check-list__item">
                        <label class="check-list__label">
                            <input class="check-list__check sr-only" type="checkbox" name="volume" value="8" checked="">
                            <span class="check-list__desc">
                                8
                                <span>(313)</span>
                            </span>
                        </label>
                    </li>
                    <li class="check-list__item">
                        <label class="check-list__label">
                            <input class="check-list__check sr-only" type="checkbox" name="volume" value="16">
                            <span class="check-list__desc">
                                16
                                <span>(461)</span>
                            </span>
                        </label>
                    </li>
                    <li class="check-list__item">
                        <label class="check-list__label">
                            <input class="check-list__check sr-only" type="checkbox" name="volume" value="32">
                            <span class="check-list__desc">
                                32
                                <span>(313)</span>
                            </span>
                        </label>
                    </li>
                    <li class="check-list__item">
                        <label class="check-list__label">
                            <input class="check-list__check sr-only" type="checkbox" name="volume" value="64">
                            <span class="check-list__desc">
                                64
                                <span>(313)</span>
                            </span>
                        </label>
                    </li>
                    <li class="check-list__item">
                        <label class="check-list__label">
                            <input class="check-list__check sr-only" type="checkbox" name="volume" value="128">
                            <span class="check-list__desc">
                                128
                                <span>(313)</span>
                            </span>
                        </label>
                    </li>
                    <li class="check-list__item">
                        <label class="check-list__label">
                            <input class="check-list__check sr-only" type="checkbox" name="volume" value="264">
                            <span class="check-list__desc">
                                264
                                <span>(313)</span>
                            </span>
                        </label>
                    </li>
                </ul>
            </fieldset>

            <button class="filter__submit button button--primery" type="submit">
                Применить
            </button>
            <button @click.prevent="onClickResetButton" class="filter__reset button button--second" type="button">
                Сбросить
            </button>
        </form>
    </aside>
</template>
<script>

import categories from '../data/categories';
import colors from '../data/colors';

export default {
    name: 'ProductsFilter',
    props: {
        filterPriceFrom: {
            type: Number,
            require: true
        },
        filterPriceTo: {
            type: Number,
            require: true
        },
        filterCategoryId: {
            type: Number,
            require: true
        },
        filterColorCode: {
            type: String,
            require: true
        },
    },
    data() {
        return {
            currentPriceFrom: this.filterPriceFrom,
            currentPriceTo: this.filterPriceTo,
            currentCategoryId: this.filterCategoryId,
            currentColorCode: this.filterColorCode,
            picked: this.filterColorCode,
            colors,
            categories
        }
    },
    watch: {
        filterPriceFrom: function () {
            this.currentPriceFrom = this.filterPriceFrom;
        },
        filterPriceTo: function () {
            this.currentPriceTo = this.filterPriceTo;
        },
        filterCategoryId: function () {
            this.currentCategoryId = this.filterCategoryId;
        },
        filterColorCode: function () {
            this.currentColorCode = this.filterColorCode;
        },
    },
    methods: {
        onclickSubmitButton() {
            this.$emit('update:filter-price-from', this.currentPriceFrom);
            this.$emit('update:filter-price-to', this.currentPriceTo);
            this.$emit('update:filter-category-id', this.currentCategoryId);
            this.$emit('update:filter-color-code', this.picked);
        },
        onClickResetButton() {
            this.$emit('update:filter-price-from', 0);
            this.$emit('update:filter-price-to', 0);
            this.$emit('update:filter-category-id', 0);
            this.$emit('update:filter-color-code', 0);
        }
    }
}
</script>
<style>
</style>
