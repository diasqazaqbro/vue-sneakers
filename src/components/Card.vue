<script setup>
defineProps({
  cardId: Number,
  title: String,
  img: String,
  price: Number
})

const isFavorite = (id) => {
  const storedItems = JSON.parse(localStorage.getItem('favoriteItems')) || []
  return storedItems.some((item) => item.id === id)
}

const addToCart = (id, title, img, price) => {
  const cartItems = JSON.parse(localStorage.getItem('cart')) || []
  const existingIndex = cartItems.findIndex((item) => item.id === id)

  if (existingIndex === -1) {
    cartItems.push({ id, title, img, price })
  } else {
    cartItems.splice(existingIndex, 1)
  }

  localStorage.setItem('cart', JSON.stringify(cartItems))
  window.location.reload()
}

const onClick = (id, title, img, price) => {
  const storedItems = JSON.parse(localStorage.getItem('favoriteItems')) || []

  const existingItemIndex = storedItems.findIndex((item) => item.id === id)

  if (existingItemIndex === -1) {
    const newItem = { id, title, img, price }
    storedItems.push(newItem)
    localStorage.setItem('favoriteItems', JSON.stringify(storedItems))
    window.location.reload()
  } else {
    storedItems.splice(existingItemIndex, 1)
    localStorage.setItem('favoriteItems', JSON.stringify(storedItems))
    window.location.reload()
  }
}
</script>

<template>
  <div
    class="relative flex flex-col w-full border border-slate-100 rounded-xl p-8 cursor-pointer transition hover:shadow-xl hover:transform hover:-translate-y-2"
  >
    <div @click="onClick(cardId, title, img, price)" class="absolute top-8 left-8">
      <img :src="isFavorite(cardId) ? '/like-2.svg' : '/like-1.svg'" alt="Favorite" />
    </div>
    <img :src="img" class="w-full" alt="Sneaker" />
    <p>{{ title }}</p>
    <div class="flex justify-between mt-5">
      <div class="flex flex-col gap-2">
        <span class="text-slate-200">Цена:</span>
        <span class="font-bold">{{ price }} руб.</span>
      </div>
      <img src="/plus.svg" alt="Plus" @click="addToCart(cardId, title, img, price)" />
    </div>
  </div>
</template>
