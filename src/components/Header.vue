<template>
  <header class="fixed top-0 left-0 right-0 z-50 bg-white/90 backdrop-blur-sm border-b border-light-gray">
    <nav class="container mx-auto px-4 h-20 flex items-center justify-between">
      <!-- Logo -->
      <router-link to="/" class="text-2xl font-display font-light tracking-wider text-primary hover:text-accent-gold transition-colors">
        Chen Wanching
      </router-link>

      <!-- Desktop Navigation -->
      <div class="hidden md:flex items-center space-x-8">
        <router-link 
          v-for="item in navItems" 
          :key="item.path" 
          :to="item.path"
          class="text-secondary hover:text-primary transition-colors relative group"
        >
          {{ item.name }}
          <span class="absolute -bottom-1 left-0 w-0 h-0.5 bg-accent-gold transition-all duration-300 group-hover:w-full"></span>
        </router-link>
      </div>

      <!-- Mobile Menu Button -->
      <button 
        @click="isMenuOpen = !isMenuOpen"
        class="md:hidden p-2 text-primary hover:text-accent-gold transition-colors"
      >
        <Bars3Icon v-if="!isMenuOpen" class="h-6 w-6" />
        <XMarkIcon v-else class="h-6 w-6" />
      </button>
    </nav>

    <!-- Mobile Menu -->
    <Transition
      enter-active-class="transition duration-200 ease-out"
      enter-from-class="transform -translate-y-full opacity-0"
      enter-to-class="transform translate-y-0 opacity-100"
      leave-active-class="transition duration-200 ease-in"
      leave-from-class="transform translate-y-0 opacity-100"
      leave-to-class="transform -translate-y-full opacity-0"
    >
      <div v-if="isMenuOpen" class="md:hidden absolute top-20 inset-x-0 bg-white/90 backdrop-blur-sm border-b border-light-gray">
        <div class="container mx-auto px-4 py-4 space-y-4">
          <router-link 
            v-for="item in navItems" 
            :key="item.path" 
            :to="item.path"
            class="block text-secondary hover:text-primary transition-colors"
            @click="isMenuOpen = false"
          >
            {{ item.name }}
          </router-link>
        </div>
      </div>
    </Transition>
  </header>
</template>

<script setup>
import { ref } from 'vue'
import { Bars3Icon, XMarkIcon } from '@heroicons/vue/24/outline'

const isMenuOpen = ref(false)

const navItems = [
  { name: 'About', path: '/about' },
  { name: 'Portfolio', path: '/works' },
  { name: 'Contact', path: '/contact' }
]
</script> 