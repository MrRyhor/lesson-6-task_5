<template>
    <div class="container">
        <products-filter v-model:brand.checkBrand="brandVal" v-model:seller.checkSeller="sellerVal" />
        <products-list :products-data="filteredProductsList" />
    </div>    
</template>

<script>
import ProductsList from './components/ProductsList.vue'
import ProductsFilter from './components/ProductsFilter.vue'
import { notebooksList } from './constants/3_data_notebooks.js'

export default {
    name: 'App',
    components: {
        ProductsList,
        ProductsFilter,
    },
    data() {
        return {
            notebooksList,
            brandVal: 'Sort by brand',
            sellerVal: 'Sort by seller',
        }
    },

    computed: {
        filteredProductsList() {
            const defaultBrandSelect = this.brandVal === 'Sort by brand'
            const defaultSellerSelect = this.sellerVal === 'Sort by seller'
            if (defaultBrandSelect && defaultSellerSelect) return notebooksList
            if (!defaultBrandSelect && !defaultSellerSelect && this.brandVal && this.sellerVal) {
                return notebooksList.filter(
                    (notebook) => notebook.brand === this.brandVal && notebook.seller === this.sellerVal
                )
            }
            if (this.brandVal && defaultSellerSelect)
                return notebooksList.filter((notebook) => notebook.brand === this.brandVal)
            if (this.sellerVal && defaultBrandSelect)
                return notebooksList.filter((notebook) => notebook.seller === this.sellerVal)
            return notebooksList
        },
    },
}
</script>

<style lang="scss">
.container {
    display: grid;
    grid-template-columns: 1fr 4fr;
    grid-template-rows: auto;
    column-gap: 40px;
}
</style>
