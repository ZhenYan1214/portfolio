<template>
  <main>
    <!-- Hero Section -->
    <section 
      ref="heroSection"
      class="min-h-screen flex items-center justify-center relative overflow-hidden bg-gradient-to-b from-white to-gray-50 transition-all duration-500"
    >
      <!-- Background Texture -->
      <div class="absolute inset-0 bg-[url('data:image/svg+xml;base64,PHN2ZyB3aWR0aD0iNjAiIGhlaWdodD0iNjAiIHZpZXdCb3g9IjAgMCA2MCA2MCIgeG1sbnM9Imh0dHA6Ly93d3cudzMub3JnLzIwMDAvc3ZnIj48ZyBmaWxsPSJub25lIiBmaWxsLXJ1bGU9ImV2ZW5vZGQiPjxwYXRoIGQ9Ik0zNiAzNGM0LjQxOCAwIDgtMy41ODIgOC04cy0zLjU4Mi04LTgtOC04IDMuNTgyLTggOCAzLjU4MiA4IDggOHoiIGZpbGw9IiMwMDAiIGZpbGwtb3BhY2l0eT0iLjAyIi8+PC9nPjwvc3ZnPg==')] opacity-5"></div>
      
      <!-- Abstract Shape -->
      <div class="absolute top-0 right-0 w-1/3 h-1/3 opacity-5">
        <svg viewBox="0 0 200 200" xmlns="http://www.w3.org/2000/svg">
          <path fill="#000000" d="M45.7,-76.4C58.8,-69.2,68.8,-55.1,75.2,-39.2C81.7,-23.3,84.7,-5.6,82.5,11.5C80.3,28.6,72.9,45.1,61.2,58.1C49.5,71.1,33.5,80.6,16.7,85.8C-0.2,91,-18,91.9,-33.5,84.9C-49,77.9,-62.3,63,-71.2,45.6C-80.1,28.2,-84.6,8.3,-81.8,-10.6C-79,-29.5,-68.9,-47.4,-54.3,-58.9C-39.7,-70.4,-20.6,-75.5,-1.3,-73.8C18,-72.2,36,-63.8,45.7,-76.4Z" transform="translate(100 100)" />
        </svg>
      </div>

      <div class="container mx-auto px-4 pt-20 text-center relative z-10">
        <!-- Role Tag -->
        <div class="animate-fade-in" style="animation-delay: 0.1s">
          <span class="inline-block text-sm tracking-widest text-gray-400 font-light uppercase mb-4">
            平面設計
          </span>
        </div>

        <h1 
          class="text-4xl md:text-6xl lg:text-7xl font-display font-light tracking-wide text-primary mb-8 animate-fade-in"
          style="animation-delay: 0.2s"
        >
        設計，讓每個想法被看見
        </h1>
        
        <p 
          class="text-xl md:text-2xl text-secondary max-w-2xl mx-auto mb-12 animate-fade-in"
          style="animation-delay: 0.4s"
        >
        這裡是我的小小作品集，
        希望能透過設計，讓每個夢想成真！
        </p>
        
        <div class="flex justify-center space-x-4 animate-fade-in" style="animation-delay: 0.8s">
          <router-link 
            to="/works" 
            class="btn-primary hover-lift hover-glow transform transition-all duration-500 hover:scale-105"
          >
            Portfolio
          </router-link>
          <router-link 
            to="/about" 
            class="btn border border-primary text-primary hover:bg-primary hover:text-white transition-all duration-500 hover:scale-105 hover-lift"
          >
            About Me
          </router-link>
        </div>
      </div>
      
      <!-- Decorative Elements -->
      <div class="absolute inset-0 -z-10">
        <div class="absolute top-1/4 left-1/4 w-64 h-64 bg-accent-gold/5 rounded-full blur-3xl"></div>
        <div class="absolute bottom-1/4 right-1/4 w-64 h-64 bg-accent-gold/5 rounded-full blur-3xl"></div>
      </div>
    </section>

    <!-- Featured Works Preview -->
    <section class="py-20 bg-light-gray">
      <div class="container mx-auto px-4">
        <h2 class="section-title text-center mb-12">Featured Works</h2>
        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
          <div 
            v-for="work in featuredWorks" 
            :key="work.id"
            class="bg-white rounded-xl shadow-md hover:shadow-xl transition-all duration-500 flex flex-col justify-between h-full overflow-hidden group animate-fade-in cursor-pointer"
            @click="openWorkDetail(work)"
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
      </div>
    </section>

    <!-- Work Detail Modal -->
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
        @click.self="closeWorkDetail"
        @keydown.esc="closeWorkDetail"
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
            @click="closeWorkDetail"
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
import { ref, onMounted } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const selectedWork = ref(null)
const heroSection = ref(null)
const modalRef = ref(null)
const imageRef = ref(null)
const contentRef = ref(null)

const featuredWorks = [
  {
    id: 1,
    title: 'Gravityless Touch｜無重力的輕盈瞬間',
    description: '一拍貼合，宛如無重力般細緻服貼。輕盈粉體，將完美膚觸輕輕釋放，讓每一次上妝都如羽毛般無痕、自然綻放無瑕光采。',
    category: '貼文設計',
    image: new URL('../assets/images/works/work-8.png', import.meta.url).href
  },
  {
    id: 2,
    title: '電商視覺設計',
    description: '以視覺說服，用美感引導消費，精準提升品牌力與轉換率。',
    category: '貼文設計',
    image: new URL('../assets/images/works/work-2.png', import.meta.url).href,
    link: '#'
  },
  {
    id: 15,
    title: 'Artisan’s Touch｜指尖流轉的溫柔工藝',
    description: '以職人精神雕琢每一寸肌理，從掌心至指尖，細膩地釋放壓力與疲憊。每一次觸感，都是對身體最真誠的聆聽與安撫。',
    category: '貼文設計',
    image: new URL('../assets/images/works/work-17.png', import.meta.url).href
  },
]

const openWorkDetail = (work) => {
  selectedWork.value = work
  document.body.style.overflow = 'hidden'
  
  // Animate background first
  gsap.fromTo('.modal-background', 
    { opacity: 0 },
    { opacity: 1, duration: 0.3 }
  )
  
  // Then animate modal
  gsap.fromTo(modalRef.value,
    { opacity: 0, scale: 0.95 },
    { opacity: 1, scale: 1, duration: 0.7, ease: 'power2.out' }
  )
  
  // Finally animate content
  gsap.fromTo(contentRef.value,
    { opacity: 0 },
    { opacity: 1, duration: 0.5, delay: 0.2 }
  )
  
  // Start image breathing animation
  gsap.to(imageRef.value, {
    scale: 1.02,
    duration: 5,
    repeat: -1,
    yoyo: true,
    ease: 'sine.inOut'
  })
}

const closeWorkDetail = () => {
  selectedWork.value = null
  document.body.style.overflow = 'auto'
}

onMounted(() => {
  // Hero section scroll animation
  gsap.to(heroSection.value, {
    scrollTrigger: {
      trigger: heroSection.value,
      start: 'top top',
      end: 'bottom top',
      scrub: true,
    },
    scale: 0.98,
    opacity: 0.8,
    backgroundColor: 'rgba(255, 255, 255, 0.9)',
  })

  // Animate sections on scroll
  gsap.utils.toArray('section').forEach((section, i) => {
    if (i === 0) return // Skip hero section
    
    gsap.from(section, {
      opacity: 0,
      y: 30,
      duration: 1,
      scrollTrigger: {
        trigger: section,
        start: 'top 80%',
        end: 'top 20%',
        toggleActions: 'play none none reverse'
      }
    })
  })
})
</script>

<style scoped>
.card {
  transition: all 0.3s ease;
}

.card:hover {
  transform: translateY(-4px);
  box-shadow: 0 20px 25px -5px rgba(0, 0, 0, 0.1), 0 10px 10px -5px rgba(0, 0, 0, 0.04);
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