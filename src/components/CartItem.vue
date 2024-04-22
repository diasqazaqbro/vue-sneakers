<script setup>
defineProps({
  img: String,
  title: String,
  price: Number,
  onClickDelete: Function,
  id: Number,
  isCart: Boolean
})

const onClick = (id, title, img, price, isCart) => {
  if (!isCart) {
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
  } else {
    const cartItems = JSON.parse(localStorage.getItem('cart')) || []
    const existingIndex = cartItems.findIndex((item) => item.id === id)

    cartItems.splice(existingIndex, 1)

    localStorage.setItem('cart', JSON.stringify(cartItems))
    window.location.reload()
  }
}
</script>

<template>
  <div class="relative flex w-full border border-slate-100 rounded-xl p-4 gap-4">
    <img :src="img" class="w-16 h-16" alt="Sneaker" />
    <div class="flex flex-col w-full">
      <p>{{ title }}</p>
      <div class="flex justify-between mt-5">
        <span class="font-bold">{{ price }} руб.</span>
        <img
          @click="onClick(id, title, img, price, isCart)"
          class="cursor-pointer opacity-30 hover:opacity-100 transition"
          src="/close.svg"
          alt="Close"
        />
      </div>
    </div>
  </div>
</template>
