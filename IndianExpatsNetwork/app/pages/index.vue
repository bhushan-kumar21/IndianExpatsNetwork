<template>
  <div class="max-w-7xl mx-auto px-4 py-12">
    <div class="text-center mb-12">
      <h1 class="text-4xl font-bold text-gray-800 mb-4">Welcome to Indians in Mexico</h1>
      <p class="text-xl text-gray-600">Your Complete Expat Guide & Community Hub</p>
    </div>

    <div class="grid md:grid-cols-4 gap-6">
      <NuxtLink
        to="/visa-govt"
        class="bg-gradient-to-br from-blue-500 to-blue-600 text-white p-8 rounded-lg shadow-lg hover:shadow-xl transition transform hover:scale-105"
      >
        <div class="text-4xl mb-4">📋</div>
        <h2 class="text-2xl font-bold mb-2">Visa & Government</h2>
        <p class="text-blue-100">Address updates, visa renewal, travel documents</p>
      </NuxtLink>

      <NuxtLink
        to="/stores"
        class="bg-gradient-to-br from-green-500 to-green-600 text-white p-8 rounded-lg shadow-lg hover:shadow-xl transition transform hover:scale-105"
      >
        <div class="text-4xl mb-4">🛒</div>
        <h2 class="text-2xl font-bold mb-2">Indian Stores</h2>
        <p class="text-green-100">Groceries, spices, and authentic Indian items</p>
      </NuxtLink>

      <NuxtLink
        to="/contacts"
        class="bg-gradient-to-br from-purple-500 to-purple-600 text-white p-8 rounded-lg shadow-lg hover:shadow-xl transition transform hover:scale-105"
      >
        <div class="text-4xl mb-4">👥</div>
        <h2 class="text-2xl font-bold mb-2">Important Contacts</h2>
        <p class="text-purple-100">English-speaking doctors, lawyers, technicians</p>
      </NuxtLink>

      <NuxtLink
        to="/banking"
        class="bg-gradient-to-br from-orange-500 to-orange-600 text-white p-8 rounded-lg shadow-lg hover:shadow-xl transition transform hover:scale-105"
      >
        <div class="text-4xl mb-4">💰</div>
        <h2 class="text-2xl font-bold mb-2">Banking & Apps</h2>
        <p class="text-orange-100">Money transfers and useful applications</p>
      </NuxtLink>

    

    </div>
  </div>
</template>