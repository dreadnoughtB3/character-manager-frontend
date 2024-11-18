<script setup lang="ts">
import { ref } from 'vue'

const isMobileMenuOpen = ref(false)

const menuItems = [
  { name: 'Home', href: '/' },
  { name: 'Characters', href: '/characters' },
]

const toggleMobileMenu = () => {
  isMobileMenuOpen.value = !isMobileMenuOpen.value
}
</script>

<template>
  <header class="fixed top-0 left-0 right-0 bg-discord-400 z-50">
    <nav class="px-4">
      <div class="flex items-center justify-between h-16">
        <!-- Logo -->
        <div class="flex-shrink-0">
          <NuxtLink to="/">
            <img src="/images/logo.jpg" class="w-auto h-8" />
          </NuxtLink>
        </div>

        <!-- Desktop Menu -->
        <div class="hidden md:block">
          <div class="ml-10 flex items-baseline space-x-4">
            <NuxtLink
              v-for="item in menuItems"
              :key="item.name"
              :to="item.href"
              class="text-gray-300 hover:text-gray-400 px-3 py-2 rounded-md text-sm font-bold"
            >
              {{ item.name }}
            </NuxtLink>
          </div>
        </div>

        <!-- Mobile menu button -->
        <div class="md:hidden">
          <button
            @click="toggleMobileMenu"
            class="inline-flex items-center justify-center p-2 rounded-md text-gray-400 hover:text-gray-500 hover:bg-discord-100 focus:outline-none focus:ring-2 focus:ring-inset focus:ring-indigo-500"
          >
            <UIcon v-if="!isMobileMenuOpen" name="i-heroicons-bars-3" class="w-6 h-6" />
          </button>
        </div>
      </div>
    </nav>

    <!-- Mobile Menu (Slide from right) -->
    <transition
      enter-active-class="transition ease-in-out duration-300 transform"
      enter-from-class="translate-x-full"
      enter-to-class="translate-x-0"
      leave-active-class="transition ease-in-out duration-300 transform"
      leave-from-class="translate-x-0"
      leave-to-class="translate-x-full"
    >
      <div v-if="isMobileMenuOpen" class="md:hidden fixed inset-y-0 right-0 max-w-xs w-full bg-discord-400 shadow-xl overflow-y-auto z-50">
        <div class="px-4 pt-5 pb-3 space-y-1">
          <div class="flex items-center justify-between mb-5">
            <button
              @click="toggleMobileMenu"
              class="text-gray-400 hover:text-gray-500 focus:ring-2 focus:ring-indigo-500"
            >
            <UIcon name="i-heroicons-x-mark" class="w-6 h-6" />
            </button>
          </div>
          <NuxtLink
            v-for="item in menuItems"
            :key="item.name"
            :to="item.href"
            class="text-gray-300 hover:text-gray-400 block px-3 py-2 border-b border-gray-400 text-base font-medium"
            @click="toggleMobileMenu"
          >
            {{ item.name }}
          </NuxtLink>
        </div>
      </div>
    </transition>

    <!-- Overlay -->
    <div
      v-if="isMobileMenuOpen"
      class="fixed inset-0 bg-black bg-opacity-25 md:hidden"
      @click="toggleMobileMenu"
    ></div>
  </header>
</template>