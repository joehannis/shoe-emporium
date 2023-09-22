<template>
  <img class="product-image" :src="product.image" />
  <div class="product-grid-item">
    <div class="product-name">{{ product.brand }}</div>
    <div class="product-price">{{ `£${product.price}` }}</div>
  </div>
</template>

<script>
export default {
  name: 'ProductGridItem',
  props: {
    product: { type: Object, required: true, default: () => ({}) }
  }
}
</script>
