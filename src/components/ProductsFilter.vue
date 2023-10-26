<template>
    <div class="container">
        <label
            >Sort by brand:
            <select class="sort" ref="brand" v-model="brandVal">
                <option>Sort by brand</option>
                <option v-for="brand in brandsList" :key="brand" :value="brand">{{ brand }}</option>
            </select>
        </label>
        <label
            >Sort by seller:
            <select class="seller" ref="seller" v-model="sellerVal">
                <option>Sort by seller</option>
                <option v-for="seller in sellersList" :key="seller" :value="seller">{{ seller }}</option>
            </select>
        </label>
    </div>
</template>
<script>
import { notebooksList } from '../constants/3_data_notebooks.js'
export default {
    name: 'ProductsFilter',

    props: {
        brand: {
            type: String,
        },
        brandModifiers: { default: () => ({}) },
        seller: {
            type: String,
        },
        sellerModifiers: { default: () => ({}) },
    },

    computed: {
        brandVal: {
            get() {
                return this.brand
            },
            set(val) {
                if (this.brandModifiers.checkBrand) this.setBrandBG(val)
                this.$emit('update:brand', val)
            },
        },
        sellerVal: {
            get() {
                return this.seller
            },
            set(val) {
                if (this.sellerModifiers.checkSeller) this.setSellerBG(val)                
                this.$emit('update:seller', val)
            },
        },
        brandsList() {
            const brandsArr = []
            notebooksList.map((notebook) => brandsArr.push(notebook.brand))
            const uniqBrands = this.getUniqArr(brandsArr)
            return uniqBrands
        },
        sellersList() {
            const sellersArr = []
            notebooksList.map((notebook) => sellersArr.push(notebook.seller))
            const uniqSellers = this.getUniqArr(sellersArr)
            return uniqSellers
        },
    },
    methods: {
        getUniqArr(arr) {
            return [...new Set(arr)].sort()
        },
        setBrandBG(val) {
            if (val === 'Sort by brand') this.$refs.brand.style.backgroundColor = 'green'            
            else this.$refs.brand.style.backgroundColor = 'transparent'
        },
        setSellerBG(val) {
            if (val === 'Sort by seller') this.$refs.seller.style.backgroundColor = 'green'            
            else this.$refs.seller.style.backgroundColor = 'transparent'
        }
    },
}
</script>
<style lang="scss" scoped>
.container {
    display: flex;
    flex-direction: column;
    gap: 20px;
    border: 2px solid black;
    padding: 10px;

    label{
        display: flex;
        flex-direction: column;
    } 
    & .sort, .seller {
        background-color: green;
    }   
}
</style>
