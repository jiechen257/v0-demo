<template>
  <div class="min-h-screen bg-white">
    <!-- Header -->
    <header class="sticky top-0 z-10 bg-white border-b">
      <div class="flex items-center justify-between px-4 h-14">
        <button class="p-2 -ml-2">
          <ChevronLeft class="w-6 h-6" />
        </button>
        <h1 class="text-lg font-semibold">SEC</h1>
        <button class="p-2 -mr-2">
          <Search class="w-6 h-6" />
        </button>
      </div>
    </header>

    <!-- Filters -->
    <div class="px-4 py-3 border-b">
      <div class="flex items-center justify-between">
        <div class="relative">
          <button class="flex items-center text-gray-600">
            Sort
            <ChevronDown class="w-4 h-4 ml-1" />
          </button>
        </div>
        <div class="flex items-center space-x-4">
          <label class="flex items-center">
            <input type="radio" name="filter" checked class="w-5 h-5 text-black" />
            <span class="ml-2">Upcoming Promotions</span>
          </label>
          <label class="flex items-center">
            <input type="radio" name="filter" class="w-5 h-5 text-black" />
            <span class="ml-2">Direct</span>
          </label>
        </div>
      </div>
    </div>

    <!-- Total Count -->
    <div class="px-4 py-3 border-b">
      <div class="flex items-center">
        <span class="text-gray-600">SEC Total</span>
        <span class="ml-2 font-semibold">{{ totalSEC }}</span>
      </div>
    </div>

    <!-- User List -->
    <div class="divide-y">
      <div v-for="user in users" :key="user.id" class="p-4">
        <!-- User Header -->
        <div class="flex items-center justify-between">
          <div class="flex items-center">
            <img :src="user.avatar" :alt="user.name" class="w-12 h-12 rounded-full" />
            <div class="ml-3">
              <div class="flex items-center">
                <span class="font-semibold">{{ user.name }}</span>
                <span class="ml-2 px-2 py-0.5 text-xs bg-black text-white rounded">SEC</span>
              </div>
              <div class="text-sm text-gray-500">Joined on {{ user.joinDate }}</div>
            </div>
          </div>
          <ChevronRight class="w-6 h-6 text-gray-400" />
        </div>

        <!-- Notification Banner -->
        <div v-if="user.notification" class="mt-3 p-3 bg-red-50 text-red-600 rounded-lg">
          {{ user.notification }}
        </div>

        <!-- Stats Grid -->
        <div class="mt-4 grid grid-cols-3 gap-4">
          <div>
            <div class="text-gray-600">SEC</div>
            <div class="text-2xl font-semibold">{{ user.stats.sec }}</div>
          </div>
          <div>
            <div class="text-gray-600">Team Resellers</div>
            <div class="text-2xl font-semibold">{{ user.stats.teamResellers }}</div>
          </div>
          <div>
            <div class="text-gray-600">Advocates</div>
            <div class="text-2xl font-semibold">{{ user.stats.advocates }}</div>
          </div>
        </div>

        <!-- Market Index -->
        <div class="mt-4 space-y-2">
          <div class="grid grid-cols-3 gap-4">
            <div>
              <div class="text-sm text-gray-600">Market Index<br />This Month (PV)</div>
              <div class="mt-1 text-xl font-semibold">{{ user.marketIndex.month }}</div>
            </div>
            <div>
              <div class="text-sm text-gray-600">Market Index<br />This Quarter (PV)</div>
              <div class="mt-1 text-xl font-semibold">{{ user.marketIndex.quarter }}</div>
            </div>
            <div>
              <div class="text-sm text-gray-600">Market Index<br />This Year (PV)</div>
              <div class="mt-1 text-xl font-semibold">{{ user.marketIndex.year }}</div>
            </div>
          </div>
        </div>

        <!-- Phone Number -->
        <div class="mt-4">
          <div class="text-gray-600">Phone Number</div>
          <div class="flex items-center mt-1">
            <span class="font-mono">{{ user.phone }}</span>
            <button class="ml-2 px-2 py-0.5 text-xs border rounded">Copy</button>
          </div>
        </div>

        <!-- Notes -->
        <div class="mt-4">
          <div class="text-gray-600">Notes</div>
          <div class="flex items-center justify-between mt-1">
            <span class="text-gray-900">{{ user.notes || 'None' }}</span>
            <Edit2 class="w-4 h-4 text-gray-400" />
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import { ChevronLeft, ChevronRight, ChevronDown, Search, Edit2 } from 'lucide-vue-next'

interface MarketIndex {
  month: string
  quarter: string
  year: string
}

interface UserStats {
  sec: number
  teamResellers: number
  advocates: number
}

interface User {
  id: number
  name: string
  avatar: string
  joinDate: string
  notification?: string
  stats: UserStats
  marketIndex: MarketIndex
  phone: string
  notes: string
}

const totalSEC = ref(30)

const users = ref<User[]>([
  {
    id: 1,
    name: 'NTXBiz User',
    avatar: '/placeholder.svg?height=48&width=48',
    joinDate: '22/02/2024',
    notification: 'Manage 2000 Resellers, 8 remaining, advancing to EEC',
    stats: {
      sec: 3,
      teamResellers: 2240,
      advocates: 56
    },
    marketIndex: {
      month: '79.05',
      quarter: '329.07',
      year: '3329.07'
    },
    phone: '176****9640',
    notes: 'Here are the filled-in notes'
  },
  {
    id: 2,
    name: 'NTXBiz User',
    avatar: '/placeholder.svg?height=48&width=48',
    joinDate: '22/02/2024',
    stats: {
      sec: 3,
      teamResellers: 2240,
      advocates: 56
    },
    marketIndex: {
      month: '79.05',
      quarter: '329.07',
      year: '3329.07'
    },
    phone: '176****9640',
    notes: 'None'
  },
  {
    id: 3,
    name: 'NTXBiz User',
    avatar: '/placeholder.svg?height=48&width=48',
    joinDate: '22/02/2024',
    stats: {
      sec: 3,
      teamResellers: 2240,
      advocates: 56
    },
    marketIndex: {
      month: '79.05',
      quarter: '329.07',
      year: '3329.07'
    },
    phone: '*********',
    notes: 'None'
  }
])
</script>

<style scoped>
input[type="radio"] {
  @apply rounded-full border-gray-300;
}
input[type="radio"]:checked {
  background-image: url("data:image/svg+xml,%3csvg viewBox='0 0 16 16' fill='white' xmlns='http://www.w3.org/2000/svg'%3e%3ccircle cx='8' cy='8' r='3'/%3e%3c/svg%3e");
}
</style>