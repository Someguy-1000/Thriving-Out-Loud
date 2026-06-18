<script setup lang="ts">
import { ref, onMounted, onUnmounted, nextTick } from 'vue';
import audibleLogo from '../assets/audible.png'
import amazonLogo from '../assets/prime.svg';

const isVisible = ref(false);
let observer: IntersectionObserver | null = null;

const banners = [
  {
    id: 1,
    title: "Amazon Prime",
    description: "Fast, free delivery & more.",
    imageUrl: amazonLogo,
    link: "#"
  },
  {
    id: 2,
    title: "Audible Free Trial",
    description: "Try Audible free for 7 days.",
    imageUrl: audibleLogo,
    link: "#"
  }
];

onMounted(() => {
  const initObserver = () => {
    const shopSection = document.getElementById('shop');
    if (shopSection) {
      observer = new IntersectionObserver((entries) => {
        entries.forEach(entry => {
          isVisible.value = entry.isIntersecting;
        });
      }, { threshold: 0.01 }); // Use a lower threshold (1%) to handle very tall elements

      observer.observe(shopSection);
      return true;
    }
    return false;
  };

  // Try immediately
  if (!initObserver()) {
    // Retry in nextTick and fallback to interval polling to handle DOM rendering timing
    nextTick(() => {
      if (!initObserver()) {
        let retries = 0;
        const interval = setInterval(() => {
          retries++;
          if (initObserver() || retries > 15) {
            clearInterval(interval);
          }
        }, 100);
      }
    });
  }
});

onUnmounted(() => {
  if (observer) observer.disconnect();
});
</script>

<template>
  <transition name="fade">
    <div v-if="isVisible">
      <!-- Desktop Side Banners -->
      <aside class="hidden xl:block">
        <!-- Left Banner (Amazon Prime) -->
        <div class="fixed left-8 top-1/2 -translate-y-1/2 w-64">
          <div class="bg-zinc-800 border border-zinc-700 rounded-2xl overflow-hidden shadow-2xl hover:border-pink-500/50 transition-all group p-8">
            <div class="h-24 flex items-center justify-center mb-8">
              <img :src="banners[0].imageUrl" :alt="banners[0].title" class="max-w-full max-h-full object-contain brightness-0 invert scale-[1.4]" />
            </div>
            <div class="text-center">
              <p class="text-[11px] font-bold text-zinc-500 uppercase tracking-widest mb-4">Official Partner</p>
              <a :href="banners[0].link" class="block text-center text-sm bg-blue-600 hover:bg-blue-500 text-white font-bold py-3 rounded-xl transition-colors">Join Amazon Prime</a>
            </div>
          </div>
        </div>

        <!-- Right Banner (Audible Free Trial) -->
        <div class="fixed right-8 top-1/2 -translate-y-1/2 w-64">
          <div class="bg-zinc-800 border border-zinc-700 rounded-2xl overflow-hidden shadow-2xl hover:border-orange-500/50 transition-all group p-8">
            <div class="h-24 flex items-center justify-center mb-8">
              <img :src="banners[1].imageUrl" :alt="banners[1].title" class="max-w-full max-h-full object-contain scale-[1.3]" />
            </div>
            <div class="text-center">
              <p class="text-[11px] font-bold text-orange-500 uppercase tracking-widest mb-4">Special Offer</p>
              <a :href="banners[1].link" class="block text-center text-sm bg-orange-600 hover:bg-orange-500 text-white font-bold py-3 rounded-xl transition-colors">Try Audible Free</a>
            </div>
          </div>
        </div>
      </aside>

      <!-- Mobile/Tablet Bottom Banners -->
      <footer class="xl:hidden bg-zinc-950 border-t border-zinc-800 p-8 pb-16">
        <div class="max-w-3xl mx-auto space-y-6">
          <h3 class="text-zinc-500 text-[11px] font-bold uppercase tracking-[0.4em] mb-8 text-center">Featured Links</h3>
          
          <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
            <!-- Mobile Prime -->
            <div class="flex items-center bg-zinc-900 border border-zinc-800 rounded-2xl p-6 gap-6 shadow-xl">
              <div class="w-20 h-20 flex items-center justify-center shrink-0">
                <img :src="banners[0].imageUrl" :alt="banners[0].title" class="max-w-full max-h-full object-contain brightness-0 invert scale-125" />
              </div>
              <div class="flex-1 min-w-0">
                <h4 class="text-white font-bold text-lg mb-1">Amazon Prime</h4>
                <a :href="banners[0].link" class="inline-block text-blue-400 text-sm font-bold hover:text-blue-300">Join Now →</a>
              </div>
            </div>

            <!-- Mobile Audible -->
            <div class="flex items-center bg-zinc-900 border border-zinc-800 rounded-2xl p-6 gap-6 shadow-xl">
              <div class="w-20 h-20 flex items-center justify-center shrink-0">
                <img :src="banners[1].imageUrl" :alt="banners[1].title" class="max-w-full max-h-full object-contain scale-125" />
              </div>
              <div class="flex-1 min-w-0">
                <h4 class="text-white font-bold text-lg mb-1">Audible Free Trial</h4>
                <a :href="banners[1].link" class="inline-block text-orange-500 text-sm font-bold hover:text-orange-400">Try Free Trial →</a>
              </div>
            </div>
          </div>
        </div>
      </footer>
    </div>
  </transition>
</template>

<style scoped>
.fade-enter-active,
.fade-leave-active {
  transition: opacity 0.5s ease, transform 0.5s ease;
}

.fade-enter-from,
.fade-leave-to {
  opacity: 0;
  transform: translateY(20px);
}

@media (min-width: 1280px) {
  .fade-enter-from,
  .fade-leave-to {
    opacity: 0;
    transform: scale(0.95);
  }
}
</style>
