<template>
  <div class="max-w-7xl mx-auto px-4 py-8">
    <h1 class="text-3xl font-bold text-gray-800 mb-8">💰 Banking & Apps</h1>

    <!-- Banks Section -->
    <div class="mb-12">
      <h2 class="text-2xl font-bold text-gray-800 mb-6">💳 Banks for Indian Transfers</h2>
      <div v-if="loadingBanks" class="text-center py-8">
        <p class="text-gray-600">Loading banks...</p>
      </div>
      <div v-else-if="errorBanks" class="bg-red-100 text-red-800 p-4 rounded mb-6">
        {{ errorBanks }}
      </div>
      <div v-else class="grid md:grid-cols-2 gap-4">
        <div v-for="bank in banks" :key="bank._id" class="bg-white rounded-lg shadow p-5 hover:shadow-lg transition">
          <h3 class="font-bold text-lg text-blue-700">{{ bank.name }}</h3>
          <p class="text-gray-600 mt-2">{{ bank.description }}</p>
          <div class="mt-3 space-y-1 text-sm text-gray-700">
            <p><strong>Rate:</strong> {{ bank.exchangeRate }}</p>
            <p><strong>Fee:</strong> {{ bank.fee }}</p>
            <p><strong>Time:</strong> {{ bank.transferTime }}</p>
          </div>
        </div>
      </div>
    </div>

    <!-- Apps Section -->
    <div>
      <h2 class="text-2xl font-bold text-gray-800 mb-6">📱 Recommended Apps & Services</h2>
      <div v-if="loadingApps" class="text-center py-8">
        <p class="text-gray-600">Loading apps...</p>
      </div>
      <div v-else-if="errorApps" class="bg-red-100 text-red-800 p-4 rounded mb-6">
        {{ errorApps }}
      </div>
      <div v-else class="grid md:grid-cols-3 gap-4">
        <div v-for="app in apps" :key="app._id" class="bg-white rounded-lg shadow p-5 hover:shadow-lg transition">
          <div class="flex items-start justify-between mb-3">
            <h3 class="font-bold text-gray-800">{{ app.name }}</h3>
            <span class="text-2xl">{{ app.icon }}</span>
          </div>
          <p class="text-gray-600 text-sm mb-2">{{ app.description }}</p>
          <p class="text-xs text-orange-600">{{ app.purpose }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const banks = ref([])
const apps = ref([])
const loadingBanks = ref(true)
const loadingApps = ref(true)
const errorBanks = ref(null)
const errorApps = ref(null)

onMounted(async () => {
  try {
    const banksResponse = await fetch('/api/banking/banks')
    banks.value = await banksResponse.json()
  } catch (err) {
    errorBanks.value = 'Failed to load banks'
    console.error(err)
  } finally {
    loadingBanks.value = false
  }

  try {
    const appsResponse = await fetch('/api/banking/apps')
    apps.value = await appsResponse.json()
  } catch (err) {
    errorApps.value = 'Failed to load apps'
    console.error(err)
  } finally {
    loadingApps.value = false
  }
})
</script>