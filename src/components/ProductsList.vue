<template>
    <div class="container">
        <product-item v-for="product in productsData" :key="product.id" :item-data="product" />
        <div class="empty" v-if="isEmpty">No results</div>
    </div>
</template>
<script>
import ProductItem from './ProductItem.vue'
export default {
    components: {
        ProductItem,
    },

    props: {
        productsData: {
            type: Array,
            default: () => [],
        },
    },

    computed: {
        isEmpty() {
            return this.productsData.length === 0
        },
    },
}
</script>
<style lang="scss" scoped>
.container {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr;
    grid-template-rows: auto;
    border: 2px solid black;
    padding: 10px;

    & .empty {
        margin: 0 auto;
        font-size: 24px;
        font-weight: 700;
    }
}
</style>
