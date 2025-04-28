<template>
  <footer class="bg-white border-t border-light-gray py-12">
    <div class="container mx-auto px-4">
      <div class="flex flex-col md:flex-row justify-between items-center">
        <div class="text-secondary text-sm mb-4 md:mb-0">
          © {{ new Date().getFullYear() }} Chen Guanqing. All rights reserved.
        </div>
        <div class="flex flex-col items-center md:flex-row md:items-center md:space-x-6">
          <div class="flex space-x-6 mb-2 md:mb-0">
            <a 
              v-for="social in socialLinks" 
              :key="social.name"
              :href="social.url"
              target="_blank"
              rel="noopener noreferrer"
              class="text-secondary hover:text-primary transition-colors group text-lg font-medium tracking-wide"
            >
              <span class="relative">
                {{ social.name }}
                <span class="absolute -bottom-1 left-0 w-0 h-0.5 bg-accent-gold transition-all duration-300 group-hover:w-full"></span>
              </span>
            </a>
          </div>

        </div>
      </div>
    </div>
  </footer>
</template>

<script setup>
const socialLinks = [
  { name: 'Canva', url: 'https://www.canva.com/design/DAGGmA7PzQ0/8tt94dzcqlPV2s9DjUdWtQ/edit?utm_content=DAGGmA7PzQ0&utm_campaign=designshare&utm_medium=link2&utm_source=sharebutton' }
]
</script> 