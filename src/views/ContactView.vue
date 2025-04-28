<template>
  <main class="py-28 bg-light-gray min-h-[70vh]">
    <section class="max-w-[700px] mx-auto px-4">
      <div class="text-center mb-14">
        <h1 class="text-4xl font-semibold tracking-wide text-primary mb-4 animate-fade-in">Let's Create Something Beautiful</h1>
        <div class="text-secondary text-base tracking-wider font-light mb-2 animate-fade-in" style="animation-delay:0.2s">
          <div>歡迎透過社群與我聯繫，開啟一場風格與故事的設計合作。</div>
          <div class="mt-1">期待與你一起打造獨特、具溫度的品牌體驗。</div>
        </div>
      </div>
      <div class="grid grid-cols-1 md:grid-cols-3 gap-8">
        <!-- IG Card -->
        <a href="https://www.instagram.com/3wanderfu1/" target="_blank" class="group bg-white rounded-2xl border border-gray-100 shadow-sm hover:shadow-lg hover:scale-105 transition-all duration-300 ease-in-out flex flex-col items-center py-10 px-6 animate-fade-in" style="animation-delay:0.3s">
          <div class="w-14 h-14 rounded-full bg-gray-100 flex items-center justify-center mb-4 transition-all duration-300 group-hover:scale-110 group-hover:shadow-lg">
            <svg class="w-7 h-7 text-gray-700 transition-colors duration-300 group-hover:text-primary" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
              <rect x="3" y="3" width="18" height="18" rx="5"/>
              <circle cx="12" cy="12" r="4"/>
              <circle cx="17" cy="7" r="1.2"/>
            </svg>
          </div>
          <div class="font-medium text-lg text-gray-900 mb-1">3wanderfu1</div>
          <div class="text-xs text-secondary tracking-wider">Instagram</div>
          <div class="text-xs text-gray-400 mt-2">作品日常</div>
        </a>
        <!-- LINE Card -->
        <div class="group bg-white rounded-2xl border border-gray-100 shadow-sm hover:shadow-lg hover:scale-105 transition-all duration-300 ease-in-out flex flex-col items-center py-10 px-6 cursor-pointer relative animate-fade-in scale-105 -translate-y-2" style="animation-delay:0.5s" @click="copyLineId" @mouseleave="showTooltip=false">
          <div class="w-14 h-14 rounded-full bg-gray-100 flex items-center justify-center mb-4 transition-all duration-300 group-hover:scale-110 group-hover:shadow-lg">
            <svg class="w-7 h-7 text-gray-700 transition-colors duration-300 group-hover:text-primary" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
              <rect x="2" y="4" width="20" height="16" rx="5"/>
              <path d="M8 12h8M8 16h4" stroke-linecap="round"/>
            </svg>
          </div>
          <div class="font-medium text-lg text-gray-900 mb-1 select-all">Wanching</div>
          <div class="text-xs text-secondary tracking-wider">LINE</div>
          <div class="text-xs text-gray-400 mt-2">快速聯繫我</div>
          <transition name="fade">
            <span v-if="showTooltip" class="absolute -top-6 left-1/2 -translate-x-1/2 bg-gray-800 text-white text-xs rounded px-3 py-1 shadow-lg z-10">已複製 LINE ID</span>
          </transition>
        </div>
        <!-- FB Card -->
        <a href="https://www.facebook.com/chen.g.qing.12" target="_blank" class="group bg-white rounded-2xl border border-gray-100 shadow-sm hover:shadow-lg hover:scale-105 transition-all duration-300 ease-in-out flex flex-col items-center py-10 px-6 animate-fade-in" style="animation-delay:0.7s">
          <div class="w-14 h-14 rounded-full bg-gray-100 flex items-center justify-center mb-4 transition-all duration-300 group-hover:scale-110 group-hover:shadow-lg">
            <svg class="w-7 h-7 text-gray-700 transition-colors duration-300 group-hover:text-primary" fill="none" stroke="currentColor" stroke-width="1.5" viewBox="0 0 24 24">
              <rect x="3" y="3" width="18" height="18" rx="5"/>
              <path d="M15 8h-2a2 2 0 0 0-2 2v2h4l-.5 2H11v6" stroke-linecap="round" stroke-linejoin="round"/>
            </svg>
          </div>
          <div class="font-medium text-lg text-gray-900 mb-1">Chen WanChing</div>
          <div class="text-xs text-secondary tracking-wider">Facebook</div>
          <div class="text-xs text-gray-400 mt-2">最新活動與案例</div>
        </a>
      </div>
    </section>
  </main>
</template>

<script setup>
import { ref } from 'vue'
const showTooltip = ref(false)
function copyLineId() {
  navigator.clipboard.writeText('Wanching')
  showTooltip.value = true
  setTimeout(() => showTooltip.value = false, 1500)
}
</script>

<style scoped>
.fade-enter-active, .fade-leave-active {
  transition: opacity 0.3s;
}
.fade-enter-from, .fade-leave-to {
  opacity: 0;
}
</style> 