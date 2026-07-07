<script setup lang="ts">
import Main from './components/Main.vue';
import Shop from './components/Shop.vue';
import AffiliateBanners from './components/AffiliateBanners.vue';
import { Analytics } from "@vercel/analytics/vue";
</script>

<template>
  <Analytics />
  <div class="scroll-smooth relative">
    <Main />
    <Shop />
    <AffiliateBanners />
  </div>
</template>

<style>
html {
  scroll-behavior: smooth;
}
</style>
