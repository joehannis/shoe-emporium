<template>
  <select v-model="selectedStockStatus" @change="handleChange">
    <option :value="null">All Products</option>
    <option :value="true">In Stock</option>
    <option :value="false">Out of Stock</option>
  </select>
</template>

<script>
export default {
  props: {
    stockStatuses: {
      type: Array,
      required: true
    }
  },
  data() {
    return {
      selectedStockStatus: null
    }
  },
  methods: {
    handleChange() {
      this.$emit('selected-stock-status', this.selectedStockStatus)
    }
  }
}
</script>
