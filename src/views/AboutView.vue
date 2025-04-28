<template>
  <main class="pt-32">
    <section class="container mx-auto px-4">
      <div class="max-w-4xl mx-auto">
        <h1 class="text-4xl md:text-5xl font-display font-light mb-8">About Me</h1>
        <div class="grid md:grid-cols-2 gap-12 items-center">
          <div class="relative">
            <div class="aspect-square rounded-full overflow-hidden">
              <img 
                src="@/assets/images/profile/me.jpg"
                alt="Chen Wanching"
                class="w-full h-full object-cover"
              />
            </div>
            <div class="absolute -inset-4 bg-accent-gold/10 rounded-full -z-10 animate-float"></div>
          </div>
          <div class="space-y-8">
            <div>
              <h2 class="text-2xl font-display font-light text-primary mb-4">
                嗨，我是 Chen Wanching，你的品牌視覺魔法師
              </h2>
              <p class="text-lg text-secondary leading-relaxed">
                專職設計，也專治「看起來不夠吸引人」的問題。
              </p>
            </div>

            <div class="space-y-4">
              <p class="text-lg text-secondary leading-relaxed italic">
                我相信，設計不只是排排字、放張圖，更是一場視覺與情感的對話。
              </p>
              <p class="text-lg text-secondary leading-relaxed">
                從 電商主視覺 到 社群貼文、從 名片設計 到 廣告海報，
                我擅長將品牌的靈魂包裝成一眼就讓人「想點進去看看」的樣子。
              </p>
            </div>

            <div>
              <p class="text-lg text-secondary leading-relaxed">
                每一張圖、每一張貼紙、每一個版面，我都用細膩的邏輯＋一點點偏執，
                讓設計不只好看，而是能打動人心、讓品牌被記住。
              </p>
            </div>

            <div class="flex flex-wrap gap-3">
              <span class="px-4 py-2 bg-gray-50 text-gray-600 rounded-full text-sm border border-gray-200">品牌設計</span>
              <span class="px-4 py-2 bg-gray-50 text-gray-600 rounded-full text-sm border border-gray-200">視覺設計</span>
              <span class="px-4 py-2 bg-gray-50 text-gray-600 rounded-full text-sm border border-gray-200">電商設計</span>
              <span class="px-4 py-2 bg-gray-50 text-gray-600 rounded-full text-sm border border-gray-200">社群設計</span>
            </div>
          </div>
        </div>
      </div>
    </section>
  </main>
</template>

<script setup>
import { onMounted } from 'vue'
import gsap from 'gsap'

onMounted(() => {
  gsap.from('.grid > *', {
    opacity: 0,
    y: 30,
    duration: 1,
    stagger: 0.2
  })
})
</script>

<style scoped>
.animate-float {
  animation: float 6s ease-in-out infinite;
}

@keyframes float {
  0%, 100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-10px);
  }
}
</style> 