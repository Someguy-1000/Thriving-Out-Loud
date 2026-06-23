<script setup lang="ts">
import { ref } from 'vue';
import subButtonImg from '../assets/Sub button (3).png';
import primeLogo from '../assets/prime.svg';

const showBanner = ref(true);

const dismissBanner = () => {
  showBanner.value = false;
};
</script>

<template>
  <div class="flex flex-col min-h-screen bg-zinc-950 text-white relative overflow-x-hidden">
    <!-- Amazon Prime Day Banner -->
    <transition name="slide-fade">
      <div 
        v-if="showBanner" 
        class="w-full bg-gradient-to-r from-[#002f54] via-[#004b75] to-[#0074a6] border-b border-[#00a8e1]/40 text-white py-1 px-6 shadow-[0_4px_25px_rgba(0,168,225,0.2)] relative overflow-hidden shrink-0 z-50"
      >
        <!-- Decorative glowing orbs in the background -->
        <div class="absolute -left-10 -top-10 w-40 h-40 bg-[#00a8e1] rounded-full blur-[80px] opacity-40 pointer-events-none"></div>
        <div class="absolute -right-10 -bottom-10 w-40 h-40 bg-[#ff9900] rounded-full blur-[80px] opacity-20 pointer-events-none"></div>

        <div class="max-w-7xl mx-auto flex items-center justify-between gap-3 relative z-10 w-full">
          <!-- Left info side -->
          <div class="flex items-center gap-2 sm:gap-4 min-w-0">
            <!-- Prime Logo (spans full height of banner and zoomed in, hidden on mobile) -->
            <div class="hidden sm:flex items-center justify-center shrink-0 h-16 w-40 overflow-hidden relative">
              <img 
                :src="primeLogo" 
                alt="Amazon Prime" 
                class="h-16 w-auto object-contain scale-[2.3] origin-center brightness-0 invert select-none drop-shadow-[0_2px_12px_rgba(255,255,255,0.25)]" 
              />
            </div>
            
            <div class="hidden sm:block h-10 w-[1px] bg-white/20 shrink-0"></div>
            
            <div class="flex items-center gap-2 min-w-0 whitespace-nowrap">
              <span class="inline-flex items-center gap-1.5 bg-[#ff9900] text-zinc-950 font-black uppercase text-[10px] sm:text-[11px] md:text-xs tracking-wider px-2.5 py-1 rounded shadow-md border border-[#ff9900]/30 animate-pulse shrink-0">
                <span class="w-1 h-1 rounded-full bg-zinc-950"></span>
                Prime Days
              </span>
              <p class="hidden sm:block text-sm md:text-base font-semibold tracking-wide text-zinc-100 drop-shadow-sm truncate">
                Exclusive deals are live!
              </p>
            </div>
          </div>

          <!-- Right CTA & Close side (in right corner) -->
          <div class="flex items-center gap-2.5 sm:gap-3 shrink-0 py-2.5">
            <a 
              href="#shop" 
              class="inline-flex items-center gap-1.5 text-[11px] sm:text-xs font-bold uppercase tracking-wider bg-white hover:bg-amber-400 hover:text-zinc-950 text-[#004b75] px-3.5 py-2 sm:px-5 sm:py-2.5 rounded-full shadow-[0_2px_8px_rgba(0,0,0,0.15)] transition-all duration-300 transform hover:scale-105 active:scale-95"
            >
              Shop Deals
              <svg xmlns="http://www.w3.org/2000/svg" class="h-3 w-3 sm:h-3.5 sm:w-3.5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2.5">
                <path stroke-linecap="round" stroke-linejoin="round" d="M14 5l7 7m0 0l-7 7m7-7H3" />
              </svg>
            </a>

            <!-- Dismiss button -->
            <button 
              @click="dismissBanner" 
              class="text-white/60 hover:text-white p-1 rounded-full hover:bg-white/10 transition-colors duration-200" 
              aria-label="Dismiss banner"
            >
              <svg xmlns="http://www.w3.org/2000/svg" class="h-4.5 w-4.5 sm:h-5 sm:w-5" fill="none" viewBox="0 0 24 24" stroke="currentColor" stroke-width="2">
                <path stroke-linecap="round" stroke-linejoin="round" d="M6 18L18 6M6 6l12 12" />
              </svg>
            </button>
          </div>
        </div>
      </div>
    </transition>

    <!-- Main Content -->
    <div class="flex-grow flex flex-col justify-center items-center p-6 relative">
      <!-- Ambient background decoration to fit the premium theme -->
      <div class="absolute w-96 h-96 -top-10 -left-10 bg-pink-500/10 rounded-full blur-[120px] pointer-events-none"></div>
      <div class="absolute w-96 h-96 -bottom-10 -right-10 bg-purple-500/10 rounded-full blur-[120px] pointer-events-none"></div>
      
      <div class="max-w-4xl w-full text-center space-y-8 relative z-10">
        <!-- Image/Logo section -->
        <div class="flex justify-center mb-8">
          <a href="https://www.tiktok.com/@thenikkiejones?_r=1&_t=ZT-97K4i9Mvkr8" target="_blank" rel="noopener noreferrer" class="hover:scale-105 active:scale-95 transition-transform block">
            <img :src="subButtonImg" alt="The Nikkie Jones" class="w-58 h-58 object-contain rounded-full border-4 border-pink-500 shadow-[0_0_20px_rgba(236,72,153,0.5)]" />
          </a>
        </div>

        <!-- Title & Tagline -->
        <div class="space-y-4">
          <h1 class="font-roboto text-[8.5vw] md:text-7xl lg:text-8xl font-black tracking-tighter uppercase italic leading-none">
            <span class="block whitespace-nowrap">Thriving Out Loud</span>
            <span class="block text-pink-500 whitespace-nowrap">Online Shop</span>
          </h1>
          
          <p class="text-xl md:text-2xl font-light tracking-[0.2em] uppercase text-zinc-400">
            The Nikkie Jones Collection
          </p>
        </div>

        <!-- Call to action -->
        <div class="pt-8">
          <a 
            href="#shop"
            class="inline-block px-8 py-3 bg-pink-600 hover:bg-pink-500 text-white font-bold rounded-full transition-all transform hover:scale-105 active:scale-95 shadow-lg"
          >
            Shop Now
          </a>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped>
/* Transition animations for banner dismissal */
.slide-fade-enter-active,
.slide-fade-leave-active {
  transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
}

.slide-fade-enter-from,
.slide-fade-leave-to {
  transform: translateY(-100%);
  opacity: 0;
}
</style>