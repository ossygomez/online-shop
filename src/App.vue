<template>
  <header>
    <div class="cart-items" @click="router.push({ name: 'CartView' })">
      <p>Items in Cart: {{ store.cart.length }}</p>
    </div>
  </header>
  <main>
    <RouterView />
  </main>
</template>

<script setup>
import router from './router'
import { productsStore } from '@/stores/products'

const store = productsStore()
</script>

<style scoped></style>
