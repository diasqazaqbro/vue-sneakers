<script setup lang="ts">
import { PropType } from 'vue'
import Card from './Card.vue'

interface Item {
  id: number
  title: string
  price: number
  imageUrl: string
}

const props = defineProps({
  items: Array as PropType<Item[]>
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
