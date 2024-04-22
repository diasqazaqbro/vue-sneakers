<script setup>
import { inject } from 'vue'
import CartItem from './CartItem.vue'
const showFavorite = inject('showFavorite')

const favoriteItems = JSON.parse(localStorage.getItem('favoriteItems')) || []
</script>

<template>
  <div class="fixed z-10 top-0 h-full w-full bg-black opacity-70" />
  <div
    class="flex flex-col justify-between fixed h-full z-10 top-0 h-full right-0 w-96 bg-white px-10 py-7"
  >
    <h2 class="text-2xl font-bold mb-10 flex items-center gap-5">
      <svg
        @click="showFavorite(false)"
        class="rotate-180 hover:-translate-x-1 opacity-30 hover:opacity-100 transition cursor-pointer"
        width="16"
        height="14"
        viewBox="0 0 16 14"
        fill="none"
        xmlns="http://www.w3.org/2000/svg"
      >
        <path
          d="M1 7H14.7143"
          stroke="black"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
        <path
          d="M8.71436 1L14.7144 7L8.71436 13"
          stroke="black"
          stroke-width="2"
          stroke-linecap="round"
          stroke-linejoin="round"
        />
      </svg>
      Закладки
    </h2>
    <div class="flex flex-col flex-1 justify-between">
      <div class="flex flex-col gap-5">
        <CartItem
          v-for="(item, index) in favoriteItems"
          :key="index"
          :id="item.id"
          :title="item.title"
          :price="item.price"
          :img="item.img"
        />
      </div>
    </div>
  </div>
</template>
