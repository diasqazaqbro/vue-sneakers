<script setup>
import CardList from '@/components/CardList.vue'
import { onMounted, reactive, ref, watch } from 'vue'
import Header from '../components/Header.vue'
import axios from 'axios'

const items = ref([])
const filters = reactive({
  sortBy: 'title',
  searchQuery: ''
})

const fetchItems = async () => {
  try {
    const params = {
      sortBy: filters.sortBy,
      title: '*'
    }

    if (filters.searchQuery) {
      params.title = `*${filters.searchQuery}`
    }
    console.log(params)
    const { data } = await axios.get('https://9b4d3ba68b55a421.mokky.dev/items', { params })
    items.value = data
  } catch (e) {
    console.log(e)
  }
}

const onChangeSelect = (event) => {
  filters.sortBy = event.target.value
}
const onChangeSearch = (event) => {
  filters.searchQuery = event.target.value
  console.log(event.target.value)
}

onMounted(() => {
  fetchItems()
})

watch(filters, fetchItems)
</script>

<template>
  <div class="bg-white w-3/5 m-auto rounded-xl shadow-xl shadow-grey-200 mt-20">
    <Header />
    <div class="p-10">
      <div class="flex justify-between items-center mb-10">
        <h1 class="text-3xl font-bold">Все кроссовки</h1>
        <div class="flex items-center gap-4">
          <select
            @change="onChangeSelect"
            class="py-2 px-3 border border-gray-200 focus:border-gray-400 rounded-md focus:outline-none"
          >
            <option value="name">По названию</option>
            <option value="price">По цене (дешевые)</option>
            <option value="-price">По цене (дорогие)</option>
          </select>
          <div class="relative">
            <input
              @change="onChangeSearch"
              type="text"
              class="border border-gray-200 rounded-md py-2 pl-10 pr-4 focus:outline-none focus:border-gray-400"
              placeholder="Поиск..."
            />
            <div class="absolute inset-y-0 left-0 pl-3 flex items-center pointer-events-none">
              <img src="/search.svg" />
            </div>
          </div>
        </div>
      </div>
      <CardList :items="items" />
    </div>
  </div>
</template>
