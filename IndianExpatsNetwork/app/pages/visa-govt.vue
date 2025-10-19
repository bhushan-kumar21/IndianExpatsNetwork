<template>
  <div class="max-w-7xl mx-auto px-4 py-8">
    <h1 class="text-3xl font-bold text-gray-800 mb-8">📋 Visa & Government Information</h1>

    <div v-if="loading" class="text-center py-12">
      <p class="text-gray-600">Loading information...</p>
    </div>

    <div v-else-if="error" class="bg-red-100 text-red-800 p-4 rounded mb-6">
      {{ error }}
    </div>

    <div v-else class="grid md:grid-cols-2 gap-6">
      <div v-for="item in govtData" :key="item._id" class="bg-white rounded-lg shadow p-6 hover:shadow-lg transition">
        <div class="flex items-start">
          <span class="text-3xl mr-4">{{ item.icon }}</span>
          <div class="flex-1">
            <h3 class="text-xl font-bold text-gray-800">{{ item.title }}</h3>
            <p class="text-gray-600 mt-2">{{ item.description }}</p>
            <div class="mt-4 space-y-2">
              <div v-for="(step, idx) in item.steps" :key="idx" class="text-sm text-gray-700">
                <strong>{{ idx + 1 }}.</strong> {{ step }}
              </div>
            </div>
            <a v-if="item.link" :href="item.link" target="_blank" class="text-orange-600 hover:text-orange-700 mt-4 inline-block font-medium">
              Learn More →
            </a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const govtData = ref([])
const loading = ref(true)
const error = ref(null)

onMounted(async () => {
  try {
    const response = await fetch('/api/govt')
    govtData.value = await response.json()
  } catch (err) {
    error.value = 'Failed to load government information'
    console.error(err)
  } finally {
    loading.value = false
  }
})
</script>