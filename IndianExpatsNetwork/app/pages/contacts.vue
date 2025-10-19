<template>
  <div class="max-w-7xl mx-auto px-4 py-8">
    <h1 class="text-3xl font-bold text-gray-800 mb-8">👥 Important Contacts</h1>

    <div v-if="loading" class="text-center py-12">
      <p class="text-gray-600">Loading contacts...</p>
    </div>

    <div v-else-if="error" class="bg-red-100 text-red-800 p-4 rounded mb-6">
      {{ error }}
    </div>

    <div v-else class="grid md:grid-cols-2 gap-6">
      <div v-for="contact in contacts" :key="contact._id" class="bg-white rounded-lg shadow p-6 hover:shadow-lg transition">
        <div class="flex items-start justify-between">
          <div>
            <div class="flex items-center mb-2">
              <span class="text-2xl mr-3">{{ contact.icon }}</span>
              <h3 class="text-lg font-bold text-gray-800">{{ contact.name }}</h3>
            </div>
            <p class="text-sm text-green-600 font-medium mb-3">{{ contact.category }}</p>
            <div class="space-y-2 text-sm text-gray-700">
              <div v-if="contact.phone">
                <strong>Phone:</strong> {{ contact.phone }}
              </div>
              <div v-if="contact.email">
                <strong>Email:</strong> {{ contact.email }}
              </div>
              <div v-if="contact.address">
                <strong>Address:</strong> {{ contact.address }}
              </div>
              <div v-if="contact.languages">
                <strong>Languages:</strong> {{ contact.languages }}
              </div>
            </div>
          </div>
          <div class="text-xs bg-orange-100 text-orange-800 px-2 py-1 rounded">
            English ✓
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const contacts = ref([])
const loading = ref(true)
const error = ref(null)

onMounted(async () => {
  try {
    const response = await fetch('/api/contacts')
    contacts.value = await response.json()
  } catch (err) {
    error.value = 'Failed to load contacts'
    console.error(err)
  } finally {
    loading.value = false
  }
})
</script>