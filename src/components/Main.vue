<script setup lang="ts">
import subButtonImg from '../assets/Sub button (3).png';
</script>

<template>
  <div class="flex flex-col min-h-screen justify-center items-center bg-zinc-950 text-white p-6">
    <div class="max-w-4xl w-full text-center space-y-8">
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
</template>

<style scoped>
/* Any additional custom styles if needed, though Tailwind 4 handles most */
</style>