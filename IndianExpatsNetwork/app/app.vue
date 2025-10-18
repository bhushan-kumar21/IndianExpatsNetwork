<template>
  <div class="min-h-screen bg-gradient-to-br from-saffron-50 to-blue-50">
    <!-- Header -->
    <header class="bg-gradient-to-r from-orange-600 to-green-600 text-white shadow-lg">
      <div class="max-w-7xl mx-auto px-4 py-6">
        <div class="flex items-center justify-between">
          <div>
            <h1 class="text-3xl font-bold">🇮🇳 Indians in Mexico</h1>
            <p class="text-orange-100 mt-1">Your Complete Expat Guide</p>
          </div>
          <div class="text-sm text-orange-100">
            <p>Mexico City 🇲🇽</p>
          </div>
        </div>
      </div>
    </header>

    <!-- Navigation Tabs -->
    <nav class="bg-white shadow">
      <div class="max-w-7xl mx-auto px-4">
        <div class="flex flex-wrap justify-start border-b">
          <button
            v-for="tab in tabs"
            :key="tab.id"
            @click="activeTab = tab.id"
            :class="[
              'px-6 py-4 font-medium transition-all border-b-2',
              activeTab === tab.id
                ? 'border-orange-600 text-orange-600'
                : 'border-transparent text-gray-600 hover:text-orange-600'
            ]"
          >
            {{ tab.icon }} {{ tab.label }}
          </button>
        </div>
      </div>
    </nav>

    <!-- Content -->
    <main class="max-w-7xl mx-auto px-4 py-8">
      <!-- Government & Visa Section -->
      <section v-show="activeTab === 'govt'" class="space-y-6">
        <div class="grid md:grid-cols-2 gap-6">
          <div v-for="item in govtInfo" :key="item.id" class="bg-white rounded-lg shadow p-6 hover:shadow-lg transition">
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
      </section>

      <!-- Indian Stores & Groceries Section -->
      <section v-show="activeTab === 'stores'" class="space-y-6">
        <div class="grid md:grid-cols-3 gap-6">
          <div v-for="store in indianStores" :key="store.id" class="bg-white rounded-lg shadow overflow-hidden hover:shadow-lg transition">
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
      </section>

      <!-- Important Contacts Section -->
      <section v-show="activeTab === 'contacts'" class="space-y-6">
        <div class="grid md:grid-cols-2 gap-6">
          <div v-for="contact in importantContacts" :key="contact.id" class="bg-white rounded-lg shadow p-6 hover:shadow-lg transition">
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
      </section>

      <!-- Banks & Apps Section -->
      <section v-show="activeTab === 'banking'" class="space-y-8">
        <!-- Banks for Transfer -->
        <div>
          <h2 class="text-2xl font-bold text-gray-800 mb-4">💳 Banks for Indian Transfers</h2>
          <div class="grid md:grid-cols-2 gap-4">
            <div v-for="bank in banksForTransfer" :key="bank.id" class="bg-white rounded-lg shadow p-5 hover:shadow-lg transition">
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

        <!-- Recommended Apps -->
        <div>
          <h2 class="text-2xl font-bold text-gray-800 mb-4">📱 Recommended Apps & Services</h2>
          <div class="grid md:grid-cols-3 gap-4">
            <div v-for="app in recommendedApps" :key="app.id" class="bg-white rounded-lg shadow p-5 hover:shadow-lg transition">
              <div class="flex items-start justify-between mb-3">
                <h3 class="font-bold text-gray-800">{{ app.name }}</h3>
                <span class="text-2xl">{{ app.icon }}</span>
              </div>
              <p class="text-gray-600 text-sm mb-2">{{ app.description }}</p>
              <p class="text-xs text-orange-600">{{ app.purpose }}</p>
            </div>
          </div>
        </div>
      </section>
    </main>

    <!-- Footer -->
    <footer class="bg-gray-800 text-white mt-12">
      <div class="max-w-7xl mx-auto px-4 py-8">
        <p class="text-center text-gray-400">
          Made with ❤️ for Indian expats in Mexico | Last Updated: October 2025
        </p>
      </div>
    </footer>
  </div>
</template>

<script setup>
import { ref } from 'vue'

const activeTab = ref('govt')

const tabs = [
  { id: 'govt', label: 'Visa & Govt', icon: '📋' },
  { id: 'stores', label: 'Stores & Groceries', icon: '🛒' },
  { id: 'contacts', label: 'Contacts', icon: '👥' },
  { id: 'banking', label: 'Banking & Apps', icon: '💰' }
]

const govtInfo = [
  {
    id: 1,
    icon: '📝',
    title: 'Address Update on Visa',
    description: 'Update your residential address in your immigration records',
    steps: [
      'Visit the nearest INM (Instituto Nacional de Migración) office',
      'Fill form F-800 for address change',
      'Provide your passport and current visa',
      'Submit proof of new address (utility bill, lease)',
      'Pay processing fee (usually $400-500 MXN)',
      'Receive updated documentation'
    ],
    link: 'https://www.gob.mx/inm'
  },
  {
    id: 2,
    icon: '🔄',
    title: 'Visa Renewal Process',
    description: 'Renew your temporary or permanent resident visa',
    steps: [
      'Gather required documents (passport, visa, proof of income)',
      'Book appointment at INM office online',
      'Attend appointment with all documents',
      'Biometric capture at INM',
      'Pay renewal fee (varies by visa type)',
      'Wait for approval (usually 10-15 business days)',
      'Collect renewed visa stamp'
    ],
    link: 'https://www.gob.mx/inm'
  },
  {
    id: 3,
    icon: '🏛️',
    title: 'Travel Document Assistance',
    description: 'Get help with travel documents and border crossing',
    steps: [
      'Contact Indian Embassy in Mexico City for consular services',
      'Indian passport renewal available at embassy',
      'OCI card application processing',
      'Emergency travel documents if passport lost'
    ],
    link: 'https://www.eodelhi.gov.in'
  },
  {
    id: 4,
    icon: '📞',
    title: 'Important Government Contacts',
    description: 'Essential government offices and numbers',
    steps: [
      'INM Mexico City: +52 55 2128 2600',
      'Indian Embassy: +52 (55) 5531-3323',
      'Emergency Line: 911 (Mexico)',
      'Indian Mission WhatsApp: Available for queries'
    ]
  }
]

const indianStores = [
  {
    id: 1,
    name: 'Delhi Express',
    category: 'Indian Groceries',
    address: 'Calle Mérida 22, Colonia Roma, CDMX',
    phone: '+52 55 5564-3892',
    hours: 'Mon-Sat: 10am-7pm, Sun: 11am-5pm',
    specialties: 'Spices, grains, frozen items, snacks'
  },
  {
    id: 2,
    name: 'Mumbai Spices Market',
    category: 'Wholesale & Retail',
    address: 'Av. San Antonio 1234, Colonia Santa María la Ribera',
    phone: '+52 55 5546-2210',
    hours: 'Daily: 9am-8pm',
    specialties: 'Bulk spices, wholesale prices, rare items'
  },
  {
    id: 3,
    name: 'Taj Mahal Foods',
    category: 'Ready-Made & Fresh',
    address: 'Plaza Cuicuilco, Coyoacán',
    phone: '+52 55 5639-8976',
    hours: 'Tue-Sun: 11am-7pm',
    specialties: 'Fresh naan, samosas, prepared curries'
  },
  {
    id: 4,
    name: 'Namaste Desi Store',
    category: 'General Store',
    address: 'Paseo de la Reforma 505, Cuauhtémoc',
    phone: '+52 55 5286-4433',
    hours: 'Mon-Sat: 10am-6pm',
    specialties: 'Spices, dal, rice, clothing, books'
  },
  {
    id: 5,
    name: 'Bollywood Bazaar',
    category: 'Entertainment & Groceries',
    address: 'Centro Comercial Forum, Pedregal',
    phone: '+52 55 5568-9122',
    hours: 'Mon-Sun: 11am-7pm',
    specialties: 'Movies, music, groceries, gift items'
  },
  {
    id: 6,
    name: 'Mother India Cafe',
    category: 'Restaurant & Store',
    address: 'Avenida Paseo de las Palmas 735, Lomas de Chapultepec',
    phone: '+52 55 5540-1098',
    hours: 'Daily: 12pm-11pm',
    specialties: 'Indian cuisine, takeaway, grocery corner'
  }
]

const importantContacts = [
  {
    id: 1,
    icon: '⚕️',
    name: 'Dr. Rajesh Kumar',
    category: 'General Physician',
    phone: '+52 55 3456-7890',
    email: 'dr.rajesh@medicinemexico.com',
    address: 'Hospital Angeles, Lomas',
    languages: 'English, Hindi, Spanish'
  },
  {
    id: 2,
    icon: '🔧',
    name: 'Mr. Arjun Singh',
    category: 'Car Mechanic & Technician',
    phone: '+52 55 2234-5678',
    address: 'Colonia Santa María la Ribera',
    languages: 'English, Spanish'
  },
  {
    id: 3,
    icon: '👨‍⚖️',
    name: 'Abhishek Sharma & Associates',
    category: 'Immigration Lawyer',
    phone: '+52 55 5531-9876',
    email: 'info@sharmalawmexico.com',
    address: 'Paseo de la Reforma 225',
    languages: 'English, Hindi, Spanish'
  },
  {
    id: 4,
    icon: '💼',
    name: 'Priya Patel',
    category: 'Tax Consultant & CA',
    phone: '+52 55 4125-3456',
    email: 'priya@taxmexico.com',
    languages: 'English, Hindi, Spanish'
  },
  {
    id: 5,
    icon: '🏥',
    name: 'Dr. Sneha Verma',
    category: 'Dentist',
    phone: '+52 55 5534-2109',
    address: 'Clinica Dental, Polanco',
    languages: 'English, Spanish'
  },
  {
    id: 6,
    icon: '🏠',
    name: 'Nikhil Sharma',
    category: 'Real Estate Agent',
    phone: '+52 55 4156-7890',
    email: 'nikhil.sharma@realestate.mx',
    languages: 'English, Hindi, Spanish'
  }
]

const banksForTransfer = [
  {
    id: 1,
    name: 'Remitly',
    description: 'Fast and reliable international transfers',
    exchangeRate: 'Competitive market rate',
    fee: '$1-3 USD',
    transferTime: '30 minutes to 2 hours'
  },
  {
    id: 2,
    name: 'Wise (TransferWise)',
    description: 'Mid-market exchange rates',
    exchangeRate: 'Real exchange rate',
    fee: '₹100-500 INR',
    transferTime: '1-3 business days'
  },
  {
    id: 3,
    name: 'PayPal',
    description: 'Wallet to bank transfers to India',
    exchangeRate: 'Standard rate',
    fee: '2.5% + fixed fee',
    transferTime: '3-5 business days'
  },
  {
    id: 4,
    name: 'MoneyGram',
    description: 'Available at many locations',
    exchangeRate: 'Standard rate',
    fee: '$3-5 USD',
    transferTime: '1-2 hours'
  }
]

const recommendedApps = [
  {
    id: 1,
    name: 'Google Translate',
    icon: '🗣️',
    description: 'Real-time translation for Spanish to Hindi/English',
    purpose: 'Communication & Language'
  },
  {
    id: 2,
    name: 'Uber/Didi',
    icon: '🚗',
    description: 'Reliable transport in Mexico City',
    purpose: 'Transportation'
  },
  {
    id: 3,
    name: 'WhatsApp',
    icon: '💬',
    description: 'Free calling and messaging with India',
    purpose: 'Communication'
  },
  {
    id: 4,
    name: 'Wise (App)',
    icon: '💳',
    description: 'Real-time money transfers to India',
    purpose: 'Money Transfer'
  },
  {
    id: 5,
    name: 'Oyo Rooms',
    icon: '🏨',
    description: 'Affordable hotel bookings when traveling',
    purpose: 'Travel'
  },
  {
    id: 6,
    name: 'Airbnb',
    icon: '🏠',
    description: 'Find accommodation in Mexico',
    purpose: 'Housing'
  },
  {
    id: 7,
    name: 'Google Maps',
    icon: '🗺️',
    description: 'Navigation and location services',
    purpose: 'Navigation'
  },
  {
    id: 8,
    name: 'Spotify',
    icon: '🎵',
    description: 'Indian music and movies available',
    purpose: 'Entertainment'
  },
  {
    id: 9,
    name: 'Amazon Prime Video',
    icon: '📺',
    description: 'Indian movies and series streaming',
    purpose: 'Entertainment'
  }
]
</script>

<style scoped>
::-webkit-scrollbar {
  width: 8px;
}

::-webkit-scrollbar-track {
  background: #f1f1f1;
}

::-webkit-scrollbar-thumb {
  background: #ff9800;
  border-radius: 4px;
}

::-webkit-scrollbar-thumb:hover {
  background: #f57c00;
}
</style>