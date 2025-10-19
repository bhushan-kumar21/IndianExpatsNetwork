<template>
  <div class="max-w-7xl mx-auto px-4 py-8">
    <h1 class="text-3xl font-bold text-gray-800 mb-8">🛒 Indian Stores & Groceries</h1>

    <div v-if="loading" class="text-center py-12">
      <p class="text-gray-600">Loading stores...</p>
    </div>

    <div v-else-if="error" class="bg-red-100 text-red-800 p-4 rounded mb-6">
      {{ error }}
    </div>

    <div v-else class="grid md:grid-cols-3 gap-6">
      <div v-for="store in stores" :key="store._id" class="bg-white rounded-lg shadow overflow-hidden hover:shadow-lg transition">
        <div class="bg-green-600 text-white p-4">
          <h3 class="text-lg font-bold">{{ store.name }}</h3>
          <p class="text-green-100 text-sm">{{ store.category }}</p>
        </div>
        <div class="p-4 space-y-3">
          <div class="flex items-start">
            <span class="text-orange-600 mr-2">📍</span>
            <p class="text-sm text-gray-700">{{ store.address }}</p>
          </div>
          <div class="flex items-start">
            <span class="text-orange-600 mr-2">📱</span>
            <p class="text-sm text-gray-700">{{ store.phone }}</p>
          </div>
          <div v-if="store.hours" class="flex items-start">
            <span class="text-orange-600 mr-2">🕒</span>
            <p class="text-sm text-gray-700">{{ store.hours }}</p>
          </div>
          <div v-if="store.specialties" class="flex items-start">
            <span class="text-orange-600 mr-2">✨</span>
            <p class="text-sm text-gray-700">{{ store.specialties }}</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const stores = ref([])
const loading = ref(true)
const error = ref(null)

onMounted(async () => {
  try {
    const response = await fetch('/api/stores')
    stores.value = await response.json()
  } catch (err) {
    error.value = 'Failed to load stores'
    console.error(err)
  } finally {
    loading.value = false
  }
})
</script>