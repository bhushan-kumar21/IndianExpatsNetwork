<template>
  <nav class="bmin-h-screen bg-gradient-to-br from-saffron-50 to-blue-50 top-0 z-50">
     <header class="bg-gradient-to-r from-orange-600 to-green-600 text-white shadow-lg">
    <div class="max-w-7xl mx-auto px-4">
      <div class="flex justify-between items-center">
        <NuxtLink to="/" class="flex items-center py-4">
          <span class="text-2xl font-bold text-blue-600">🇮🇳</span>
          <span class="text-xl font-bold text-gray-800 ml-2">Indians in Mexico</span>
        </NuxtLink>
       
        <div class="flex flex-wrap justify-end gap-1">
          <NuxtLink
            to="/"
            class="px-4 py-2 rounded transition hover:bg-orange-100 text-gray-700 hover:text-orange-600"
          >
            Home
          </NuxtLink>


           <NuxtLink
            to="/About-Page"
            class="px-4 py-2 rounded transition hover:bg-orange-100 text-gray-700 hover:text-orange-600"
          >
            About Page
          </NuxtLink>
        </div>
      </div>
    </div>
     </header>
  </nav>
  
</template>