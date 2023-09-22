<template>
  <div class="brand-selecter">
    <div v-for="brand in uniqueBrands" :key="brand">
      <label class="brand-element">
        <input type="checkbox" :value="brand" v-model="selectedBrands" @change="handleChange" />
        {{ brand }}
      </label>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    products: {
      type: Array,
      required: true
    }
  },
  computed: {
    uniqueBrands() {
      const brandsSet = new Set()
      this.products.forEach((product) => {
        brandsSet.add(product.brand)
      })
      return Array.from(brandsSet)
    }
  },
  data() {
    return {
      selectedBrands: []
    }
  },
  methods: {
    handleChange() {
      this.$emit('brandSelected', this.selectedBrands)
    }
  }
}
</script>
