<template lang="html">
  <div class="products-list">
    <div
      class="product"
      v-for="product in store.products"
      :key="product.id"
      @click="goToProductPage(product.id)"
    >
      <img :src="product.thumbnail" :alt="product.title" />
      <h2>Brand: {{ product.brand }}</h2>
      <p>Description: {{ product.description }}</p>
      <p>Price: ${{ product.price }}</p>
    </div>
  </div>
</template>

<script>
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'CatalogView'
})
</script>

<script setup>
import { onMounted } from 'vue'
import { productsStore } from '@/stores/products'
import { useRouter } from 'vue-router'

const store = productsStore()
const router = useRouter()
const goToProductPage = (id) => {
  router.push({ name: 'ProductView', params: { id } })
}

onMounted(async () => {
  await store.fetchProductsFromDB()
})
</script>

<style lang="css" scoped>
.products-list {
  display: flex;
  justify-content: space-between;
  flex-wrap: wrap;
}
.product {
  cursor: pointer;
  flex-basis: 28%;
  margin: 8px;
  padding: 16px;
  box-shadow: 0 0 14px 1px #e6e6e6;
}
.product img {
  width: 70%;
}
</style>
