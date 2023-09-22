<template>
  <div id="app">
    <div class="header">
      <div class="centered-text">
        <div class="title">The Shoe Emporium</div>
      </div>
      <p class="filter-container">
        <StockFilter
          :stock-statuses="stockStatuses"
          @selected-stock-status="handleStockStatusSelected"
        />
        <span class="filters-counter">{{ counter }} products</span>
      </p>
    </div>

    <BrandFilter :products="products" @brand-selected="handleBrandSelected" />
    <div class="product-container">
      <div class="no-products" v-if="filteredProductList.length === 0">There are no products</div>

      <li class="list" v-for="product in filteredProductList" :key="product.name">
        <div class="card-container">
          <ProductGridItem :product="product" />
        </div>
      </li>
    </div>
  </div>
</template>

<script>
import ProductGridItem from './components/ProductGridItem.vue'
import products from './data/products.json'
import BrandFilter from './components/BrandFilter.vue'
import StockFilter from './components/StockFilter.vue'

export default {
  name: 'App',
  components: {
    ProductGridItem,
    BrandFilter,
    StockFilter
  },
  data() {
    return {
      products: products,
      stockStatuses: [...new Set(products.map((product) => product.isAvailable))],
      filteredProductList: products,
      selectedBrand: '',
      selectedStatus: null,
      counter: products.length
    }
  },
  methods: {
    filterProducts() {
      this.filteredProductList = this.products.filter((product) => {
        const isBrandMatch =
          this.selectedBrands.length === 0 || this.selectedBrands.includes(product.brand)
        const isStatusMatch =
          this.selectedStatus === null || product.isAvailable === this.selectedStatus
        return isBrandMatch && isStatusMatch
      })
      if (this.selectedBrands.length === 0 && this.selectedStatus === null) {
        this.filteredProductList = this.products
      }
      this.counter = this.filteredProductList.length
    },

    handleBrandSelected(selectedBrands) {
      this.selectedBrands = selectedBrands
      this.filterProducts()
    },
    handleStockStatusSelected(status) {
      this.selectedStatus = status
      this.filterProducts()
    }
  }
}
</script>
