<template>
  <footer class="bg-white border-t border-light-gray py-12">
    <div class="container mx-auto px-4">
      <div class="flex flex-col md:flex-row justify-between items-center">
        <div class="text-secondary text-sm mb-4 md:mb-0">
          © {{ new Date().getFullYear() }} Chen Guanqing. All rights reserved.
        </div>
        <div class="flex space-x-6">
          <a 
            v-for="social in socialLinks" 
            :key="social.name"
            :href="social.url"
            target="_blank"
            rel="noopener noreferrer"
            class="text-secondary hover:text-primary transition-colors group"
          >
            <span class="relative">
              {{ social.name }}
              <span class="absolute -bottom-1 left-0 w-0 h-0.5 bg-accent-gold transition-all duration-300 group-hover:w-full"></span>
            </span>
          </a>
        </div>
      </div>
    </div>
  </footer>
</template>

<script setup>
const socialLinks = [
  { name: 'LinkedIn', url: 'https://linkedin.com' },
  { name: 'Dribbble', url: 'https://dribbble.com' },
  { name: 'Behance', url: 'https://behance.net' }
]
</script> 