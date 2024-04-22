<script setup>
import { inject } from 'vue'

const showDrawer = inject('showDrawer')
const showFavorite = inject('showFavorite')

const cartNumber = () => {
  const cartItems = JSON.parse(localStorage.getItem('cart')) || []
  let totalPrice = 0

  for (const item of cartItems) {
    totalPrice += item.price
  }

  return totalPrice
}
</script>

<template>
  <header class="flex justify-between border-b border-slate-200 px-10 py-8">
    <div class="flex items-center gap-4">
      <img src="/logo.png" alt="Logo" class="w-11" />
      <div>
        <h2 class="font-bold text-xl uppercase">Vue Sneakers</h2>
        <p class="text-slate-400">Магазин лучших кроссовок</p>
      </div>
    </div>

    <ul class="flex items-center gap-10">
      <li @click="showDrawer(true)" class="flex items-center gap-3 cursor-pointer">
        <img src="/cart.svg" alt="Cart" />
        <b>{{ cartNumber() }}</b>
      </li>
      <li @click="showFavorite(true)" class="flex items-center gap-3 cursor-pointer">
        <img src="/heart.svg" alt="Favorite" />
        <span>Закладки</span>
      </li>
    </ul>
  </header>
</template>
