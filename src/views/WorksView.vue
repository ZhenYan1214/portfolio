<template>
  <main class="pt-32">
    <!-- Hero Section -->
    <section class="py-20 bg-gray-50">
      <div class="container mx-auto px-4 text-center">
        <h1 class="text-4xl md:text-5xl font-display font-light text-primary mb-6 animate-fade-in">
          我的作品，來自每一段用心的設計旅程
        </h1>
        <p class="text-xl text-secondary max-w-2xl mx-auto animate-fade-in" style="animation-delay: 0.2s">
          這裡收藏了我在不同領域裡，用設計記錄的每一次精彩。
        </p>
      </div>
    </section>

    <!-- Works Grid -->
    <section class="py-20">
      <div class="container mx-auto px-4">
        <!-- Filter Categories -->
        <div class="flex flex-wrap justify-center gap-3 mb-16">
          <button 
            v-for="category in categories" 
            :key="category"
            @click="activeCategory = category"
            :class="[
              'px-6 py-2 rounded-full text-sm tracking-wide transition-all duration-300',
              activeCategory === category 
                ? 'bg-primary text-white shadow-md' 
                : 'bg-gray-50 text-secondary hover:bg-gray-100 border border-gray-200'
            ]"
          >
            {{ category }}
          </button>
        </div>

        <!-- Works Grid -->
        <TransitionGroup 
          name="works-grid" 
          tag="div" 
          class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8"
        >
          <div 
            v-for="work in filteredWorks" 
            :key="work.id"
            class="group flex flex-col justify-between h-full"
          >
            <div 
              class="card bg-white rounded-xl shadow-sm hover:shadow-xl transition-all duration-500 flex flex-col justify-between h-full overflow-hidden cursor-pointer"
              @click="openPreview(work)"
            >
              <!-- Image -->
              <div class="relative w-full aspect-[4/3] overflow-hidden">
                <img 
                  :src="work.image" 
                  :alt="work.title"
                  class="w-full h-full object-cover transition-transform duration-500 group-hover:scale-105 group-hover:shadow-2xl"
                />
                <div class="absolute inset-0 pointer-events-none group-hover:bg-black/10 transition-colors duration-300"></div>
              </div>
              <!-- Content -->
              <div class="flex flex-col flex-1 p-6 justify-between">
                <div>
                  <h3 class="text-xl font-display font-light mb-2 text-gray-900">{{ work.title }}</h3>
                  <p class="text-secondary text-sm mb-4 line-clamp-2 min-h-[48px]">{{ work.description }}</p>
                </div>
                <div class="min-h-[40px] flex items-end">
                  <span class="inline-block text-sm px-3 py-1 bg-gray-50 text-gray-600 rounded-full border border-gray-200">
                    {{ work.category }}
                  </span>
                </div>
              </div>
            </div>
          </div>
        </TransitionGroup>
      </div>
    </section>

    <!-- Image Preview Modal -->
    <Transition
      enter-active-class="transition duration-700 ease-out"
      enter-from-class="transform opacity-0 scale-95"
      enter-to-class="transform opacity-100 scale-100"
      leave-active-class="transition duration-300 ease-in"
      leave-from-class="transform opacity-100 scale-100"
      leave-to-class="transform opacity-0 scale-95"
    >
      <div 
        v-if="selectedWork" 
        class="fixed inset-0 z-50 flex items-center justify-center p-4 bg-black/30 backdrop-blur-2xl"
        @click.self="closePreview"
        @keydown.esc="closePreview"
      >
        <!-- Background Particles -->
        <div class="modal-background absolute inset-0 opacity-0">
          <div class="absolute inset-0 bg-[url('data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNjAiIGhlaWdodD0iNjAiIHZpZXdCb3g9IjAgMCA2MCA2MCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48ZyBmaWxsPSJub25lIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiPjxwYXRoIGQ9Ik0zNiAzNGM0LjQxOCAwIDgtMy41ODIgOC04cy0zLjU4Mi04LTgtOC04IDMuNTgyLTggOCAzLjU4MiA4IDggOHoiIGZpbGw9IiMwMDAiIGZpbGwtb3BhY2l0eT0iLjAyIi8+PC9nPjwvc3ZnPg==')] opacity-5 animate-float"></div>
        </div>

        <!-- Main Modal Card -->
        <div 
          ref="modalRef"
          class="relative w-full max-w-[600px] bg-white/5 backdrop-blur-3xl rounded-3xl shadow-2xl p-8"
          style="box-shadow: 0 0 0 1px rgba(255,255,255,0.1) inset, 0 8px 32px 0 rgba(0,0,0,0.2);"
        >
          <!-- Close Button -->
          <button 
            @click="closePreview"
            class="fixed top-4 right-4 z-50 p-3 bg-white/90 backdrop-blur-sm rounded-full hover:bg-white transition-all duration-300 transform hover:scale-110 hover:shadow-lg"
          >
            <svg class="w-6 h-6 text-gray-800" fill="none" stroke="currentColor" viewBox="0 0 24 24">
              <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M6 18L18 6M6 6l12 12" />
            </svg>
          </button>

          <!-- Image Container -->
          <div 
            ref="imageRef"
            class="relative w-full aspect-[4/3] overflow-hidden rounded-2xl bg-gray-900/20 flex items-center justify-center mb-8"
          >
            <img 
              :src="selectedWork.image" 
              :alt="selectedWork.title"
              class="w-full h-full object-contain p-8 drop-shadow-md"
            />
          </div>

          <!-- Divider -->
          <div class="border-t border-white/10 mb-8"></div>

          <!-- Work Info -->
          <div 
            ref="contentRef"
            class="bg-white/10 backdrop-blur-md rounded-xl p-6 shadow-md"
          >
            <h2 class="text-2xl font-semibold tracking-wider mb-3 text-white">{{ selectedWork.title }}</h2>
            <p class="text-base text-gray-300 leading-relaxed tracking-wide mb-4 line-clamp-3">{{ selectedWork.description }}</p>
            <span class="text-xs px-3 py-1.5 bg-white/10 text-white/90 rounded-full inline-block">
              {{ selectedWork.category }}
            </span>
          </div>
        </div>
      </div>
    </Transition>
  </main>
</template>

<script setup>
import { ref, computed } from 'vue'
import { onMounted } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const categories = ['All', '貼文設計', '印刷品', 'AI設計']
const activeCategory = ref('All')
const selectedWork = ref(null)
const modalRef = ref(null)
const imageRef = ref(null)
const contentRef = ref(null)

const works = [
  {
    id: 1,
    title: 'Echoes of Distraction｜分心的回聲',
    description: '以溫柔幽默描繪數位焦慮，喚醒專注與連結的價值。',
    category: '貼文設計',
    image: new URL('../assets/images/works/work-2.png', import.meta.url).href
  },
  {
    id: 2,
    title: 'Swiped Away｜被滑走的專注力',
    description: '在科技洪流中，專注力悄悄被滑走。以輕盈筆觸描繪現代人的日常焦慮，呈現數位世界下的情緒流動。',
    category: '貼文設計',
    image: new URL('../assets/images/works/work-4.png', import.meta.url).href
  },
  {
    id: 3,
    title: 'A Bite of Dreams｜一口夢境',
    description: '用柔和筆觸打造療癒系視覺，讓品牌在日常中悄悄盛開。',
    category: '印刷品',
    image: new URL('../assets/images/works/work-3.png', import.meta.url).href
  },
  {
    id: 4,
    title: 'The First Bite of Love｜初嚐戀愛的滋味',
    description: '熱情番茄、醇厚起司與新鮮羅勒，在炙熱爐火中共舞。每一口，都是經典瑪格麗特的純粹告白，為日常注入一抹溫柔而鮮明的悸動。',
    category: '貼文設計',
    image: new URL('../assets/images/works/work-7.png', import.meta.url).href
  },
  {
    id: 5,
    title: 'Whispers of an Apple｜蘋果的呢喃',
    description: '一顆蘋果，藏著無數溫柔的想像。以輕盈手繪描摹自然，賦予日常物件新的詩意生命。',
    category: '印刷品',
    image: new URL('../assets/images/works/work-6.png', import.meta.url).href
  },
  {
    id: 6,
    title: 'Gravityless Touch｜無重力的輕盈瞬間',
    description: '一拍貼合，宛如無重力般細緻服貼。輕盈粉體，將完美膚觸輕輕釋放，讓每一次上妝都如羽毛般無痕、自然綻放無瑕光采。',
    category: '貼文設計',
    image: new URL('../assets/images/works/work-8.png', import.meta.url).href
  },
  {
    id: 7,
    title: 'A Day of Privilege｜專屬禮遇之日',
    description: '在流光中，為摯愛品牌而來的日子。專屬會員禮遇，讓每一次選擇都值得被珍藏，限時珍貴，成就每一段不凡體驗。',
    category: '貼文設計',
    image: new URL('../assets/images/works/work-9.png', import.meta.url).href
  },
  {
    id: 8,
    title: 'A Picnic of Light｜輕盈午後的野餐夢',
    description: '在暖陽與微風中，甜點、笑聲與慵懶的片刻交織成畫。AI 筆觸下的小貓，戴著夏日微笑，在野餐墊上恣意伸展，喚醒每個人心中最柔軟的夏天。',
    category: 'AI設計',
    image: new URL('../assets/images/works/work-10.png', import.meta.url).href
  },
  {
    id: 9,
    title: 'Neon Pulse｜霓光脈搏的少女覺醒',
    description: '在電光閃耀的世界裡，她以無畏之姿喚醒未來。霓虹與速度交織成新生代的節奏，每一個目光，都映照著無限可能的冒險啟程。',
    category: 'AI設計',
    image: new URL('../assets/images/works/work-11.jpg', import.meta.url).href
  },
  {
    id: 10,
    title: 'Festive Whispers｜節慶裡的微笑邀請',
    description: '在日系紅燈籠與暖湯香氣中，拋飛飛鏢、分享一碗關東煮，用遊戲和味覺編織出最柔軟的相遇時光。每個笑聲，都讓冬日市集更加溫暖。',
    category: '印刷品',
    image: new URL('../assets/images/works/work-12.png', import.meta.url).href
  },
  {
    id: 11,
    title: 'Retro Reverie｜時光派對的倒數節奏',
    description: '揉合復古情懷與青春律動，倒數的每一天，都是記憶裡最鮮明的片段。透過視覺節奏串連倒數、抽獎與感謝，讓社群互動在懷舊與期待間悄悄升溫。',
    category: '印刷品',
    image: new URL('../assets/images/works/work-13.png', import.meta.url).href
  },
  {
    id: 12,
    title: 'Retro Glitch｜嬉鬧復古的小宇宙',
    description: '以粗顆粒筆觸與鮮明配色，捕捉復古派對裡的狂歡記憶。每一枚貼紙，都是一段不羈的呢喃，讓歡笑與懷舊情緒，在指尖悄悄發酵。',
    category: '印刷品',
    image: new URL('../assets/images/works/work-14.png', import.meta.url).href
  },
  {
    id: 13,
    title: 'Moments to Collect｜時光裡的微醺印記',
    description: '以懷舊插畫搭配集點互動，將復古派對的溫度延伸至每一次舉杯、每一場笑語。設計讓參與者在集點中留下專屬於當晚的微醺記憶，凝結成獨一無二的節慶篇章。',
    category: '貼文設計',
    image: new URL('../assets/images/works/work-15.png', import.meta.url).href
  }
]

const filteredWorks = computed(() => {
  if (activeCategory.value === 'All') return works
  return works.filter(work => work.category === activeCategory.value)
})

// Optimize animations
onMounted(() => {
  // Only animate cards when they first appear
  gsap.utils.toArray('.card').forEach((card, i) => {
    gsap.from(card, {
      opacity: 0,
      y: 30,
      duration: 0.4, // Reduced duration
      delay: i * 0.05, // Reduced delay
      scrollTrigger: {
        trigger: card,
        start: 'top 80%',
        end: 'top 20%',
        toggleActions: 'play none none none' // Changed to only play once
      }
    })
  })
})

// Add loading state
const isLoading = ref(false)

const openPreview = (work) => {
  selectedWork.value = work
  document.body.style.overflow = 'hidden'
  
  // Preload image
  const img = new Image()
  img.src = work.image
  
  // Animate background first
  gsap.fromTo('.modal-background', 
    { opacity: 0 },
    { opacity: 1, duration: 0.2 } // Reduced duration
  )
  
  // Then animate modal
  gsap.fromTo(modalRef.value,
    { opacity: 0, scale: 0.95 },
    { opacity: 1, scale: 1, duration: 0.4, ease: 'power2.out' } // Reduced duration
  )
  
  // Finally animate content
  gsap.fromTo(contentRef.value,
    { opacity: 0 },
    { opacity: 1, duration: 0.3, delay: 0.1 } // Reduced duration and delay
  )
  
  // Start image breathing animation
  gsap.to(imageRef.value, {
    scale: 1.02,
    duration: 4, // Reduced duration
    repeat: -1,
    yoyo: true,
    ease: 'sine.inOut'
  })
}

const closePreview = () => {
  selectedWork.value = null
  document.body.style.overflow = 'auto'
}
</script>

<style scoped>
.card {
  transition: all 0.3s ease;
}

.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
}

.works-grid-enter-active,
.works-grid-leave-active {
  transition: all 0.5s ease;
}

.works-grid-enter-from,
.works-grid-leave-to {
  opacity: 0;
  transform: translateY(30px);
}

.works-grid-move {
  transition: transform 0.5s ease;
}

.animate-float {
  animation: float 10s ease-in-out infinite;
}

@keyframes float {
  0%, 100% {
    transform: translate(0, 0);
  }
  50% {
    transform: translate(10px, 10px);
  }
}
</style> 