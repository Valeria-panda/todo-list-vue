<template>
    <ul class="catalog__pagination pagination">
        <li class="pagination__item">
            <a class="pagination__link pagination__link--arrow pagination__link--disabled"
                aria-label="Предыдущая страница">
                <svg width="8" height="14" fill="currentColor">
                    <use xlink:href="#icon-arrow-left"></use>
                </svg>
            </a>
        </li>
        <li class="pagination__item" v-for="pageNumber in countTotalPages" :key="pageNumber">
            <a @click.prevent="paginate(pageNumber)" class="pagination__link"
                :class="{ 'pagination__link--current': pageNumber === page }">
                {{ pageNumber }}
            </a>
        </li>
        <li class="pagination__item">
            <a class="pagination__link pagination__link--arrow" href="#" aria-label="Следующая страница">
                <svg width="8" height="14" fill="currentColor">
                    <use xlink:href="#icon-arrow-right"></use>
                </svg>
            </a>
        </li>
    </ul>
</template>
<script>

export default {
    name: 'StandartPagination',
    model: {
        prop: 'page',
        event: 'paginate',
    },
    props: {
        page: {
            type: Number,
            required: true,
        },
        count: {
            type: Function,
            required: true
        },
        perPage: {
            type: Number,
            required: true
        },
    },
    computed: {
        countTotalPages() {
            return Math.ceil(this.count / this.perPage);
        }
    },
    methods: {
        paginate(page) {
            this.$emit('paginate', page);
        }
    }
}
</script>
<style>
</style>
 