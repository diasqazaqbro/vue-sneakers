<script setup>
import HomePage from './pages/Home.vue'
import Drawer from './components/Drawer.vue'
import Favorite from './components/Favorite.vue'
import { provide, ref } from 'vue'

const isDrawer = ref(false)
const isFavorite = ref(false)
const showDrawer = (arg) => {
  isDrawer.value = arg
}
const showFavorite = (arg) => {
  isFavorite.value = arg
}
const getFavorite = localStorage.getItem('cart')
console.log(getFavorite)
provide('showDrawer', showDrawer)
provide('showFavorite', showFavorite)

// provide('message', message)
</script>

<template>
  <Drawer v-if="isDrawer" />
  <Favorite v-if="isFavorite" />
  <HomePage />
</template>
