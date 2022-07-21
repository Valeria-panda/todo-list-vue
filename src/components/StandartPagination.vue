<template>
    <ul class="catalog__pagination pagination">
        <li class="pagination__item">
            <a @click.prevent="prevButton()" class="pagination__link pagination__link--arrow pagination__link--disabled"
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
            <a @click.prevent="nextButton()" class="pagination__link pagination__link--arrow" href="#"
                aria-label="Следующая страница">
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
            this.$emit('update:page', page);
        },
        nextButton() {
            this.$emit('update:page', this.page + 1);
        },
        prevButton() {
            this.$emit('update:page', this.page - 1);
        }
    }
}
</script>
<style>
.catalog__pagination {
    margin-top: auto
}

.pagination {
    margin: 0;
    padding: 0;
    list-style: none;
    display: -webkit-box;
    display: -ms-flexbox;
    display: flex;
    -webkit-box-align: center;
    -ms-flex-align: center;
    align-items: center;
    -webkit-box-pack: center;
    -ms-flex-pack: center;
    justify-content: center
}

.pagination__item:first-child {
    margin-right: 25px
}

.pagination__item:last-child {
    margin-left: 25px
}

.pagination__link {
    display: block;
    padding: 13px 3px;
    height: 40px;
    min-width: 40px;
    font-size: 16px;
    line-height: 1;
    color: #222;
    text-align: center;
    -webkit-transition: all .2s ease;
    transition: all .2s ease
}

.pagination__link[href]:not(:disabled):focus,
.pagination__link[href]:not(:disabled):hover {
    opacity: .6
}

.pagination__link--current {
    font-weight: 700
}

.pagination__link--arrow {
    border: 1px solid #e2e2e2
}

.pagination__link--disabled {
    opacity: .6;
    cursor: not-allowed
}
</style>
 