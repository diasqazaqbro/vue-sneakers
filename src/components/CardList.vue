<script setup>
import Card from './Card.vue'
const props = defineProps({
  items: Array
})
</script>

<template>
  <div class="grid grid-cols-4 gap-10">
    <Card
      v-for="item in props.items"
      :key="item.id"
      :cardId="item.id"
      :title="item.title"
      :price="item.price"
      :img="item.imageUrl"
    />
  </div>
</template>
