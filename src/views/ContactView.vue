<template>
  <main class="py-32 bg-light-gray min-h-[80vh] flex items-center">
    <section class="max-w-[480px] mx-auto px-4 w-full">
      <div class="text-center mb-14">
        <h1 class="text-4xl font-semibold tracking-wide text-primary mb-4 animate-fade-in">Let's Connect</h1>
        <div class="text-secondary text-base tracking-wider font-light mb-3 animate-fade-in" style="animation-delay:0.2s">
          歡迎與我聯繫，開啟一場風格與故事的設計合作。
        </div>
        <div class="text-gray-400 text-sm italic mb-2 animate-fade-in" style="animation-delay:0.3s">
          設計連結人與品牌，創造細節中的情感共鳴。
        </div>
      </div>
      <div class="relative flex justify-center">
        <!-- 背後超大超淡圓形光暈 -->
        <div class="absolute top-1/2 left-1/2 -translate-x-1/2 -translate-y-1/2 w-[340px] h-[340px] rounded-full bg-accent-gold blur-3xl opacity-5 -z-10"></div>
        <!-- Email Card -->
        <div class="group bg-white/90 rounded-3xl border border-gray-100 shadow-xl hover:shadow-2xl hover:scale-[1.02] transition-all duration-300 ease-in-out flex flex-col items-center py-14 px-10 cursor-pointer relative animate-fade-in" style="animation-delay:0.5s" @click="copyEmail" @mouseleave="showEmailTooltip=false">
          <div class="w-16 h-16 rounded-full bg-gradient-to-tr from-accent-gold/20 to-accent-blue/10 flex items-center justify-center mb-7 transition-all duration-300 group-hover:scale-110 group-hover:shadow-lg">
            <svg class="w-8 h-8 text-primary transition-colors duration-300 group-hover:text-accent-gold" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
              <path d="M4 4h16c1.1 0 2 .9 2 2v12c0 1.1-.9 2-2 2H4c-1.1 0-2-.9-2-2V6c0-1.1.9-2 2-2z" stroke-linecap="round" stroke-linejoin="round"/>
              <path d="M22 6l-10 7L2 6" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
          </div>
          <div class="font-medium text-xl text-gray-900 mb-2 select-all tracking-wide">wanchinggggchen@gmail.com</div>
          <div class="text-xs text-gray-400 mb-2">點擊複製</div>
          <transition name="fade">
            <span v-if="showEmailTooltip" class="absolute -top-6 left-1/2 -translate-x-1/2 bg-gray-800 text-white text-xs rounded px-3 py-1 shadow-lg z-10">已複製 Email</span>
          </transition>
          <div class="mt-6 text-xs text-gray-400 text-center tracking-wide">Available for freelance UI/UX projects and collaborations</div>
        </div>
      </div>
    </section>
  </main>
</template>

<script setup>
import { ref } from 'vue'
const showEmailTooltip = ref(false)

function copyEmail() {
  navigator.clipboard.writeText('wanchinggggchen@gmail.com')
  showEmailTooltip.value = true
  setTimeout(() => showEmailTooltip.value = false, 1500)
}
</script>

<style scoped>
.blur-3xl {
  filter: blur(64px);
}
.opacity-5 {
  opacity: 0.05;
}
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.3s;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
</style> 