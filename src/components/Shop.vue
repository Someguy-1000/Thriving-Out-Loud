<script setup lang="ts">
import { ref, computed } from 'vue';

interface Product {
  id: string;
  name: string;
  price: string;
  imageUrl: string;
  amazonUrl: string;
  category: string;
  subcategory?: string;
}

const activeCategory = ref('All');

const getImageUrl = (imgName: string) => {
  if (imgName.startsWith('http')) return imgName;
  // Use Vite's way to handle local assets
  return new URL(`../assets/products/${imgName}`, import.meta.url).href;
};

const categories = [
  {
    name: "Featured",
    items: [
      { name: "Brooks Women’s Ghost 18 Neutral Running & Walking Shoe", url: "https://amzn.to/4xBHnGu", img: "Brooks Women’s Ghost 18 Neutral Running & Walking Shoe.jpg" },
      { name: "LUMIFY Eye Drops for Red Eyes, Redness Reliever", url: "https://amzn.to/4ewc8UT", img: "LUMIFY Eye Drops for Red Eyes, Redness Reliever.jpg" },
      { name: "Takeya Deluxe Cold Brew Coffee Maker", url: "https://amzn.to/4uAYt4F", img: "Takeya Deluxe Cold Brew Coffee Maker.jpg" },
      { name: "Owala FreeSip Insulated Stainless Steel Water Bottle", url: "https://amzn.to/4uGu70C", img: "Owala FreeSip Insulated Stainless Steel Water Bottle.jpg" },
      { name: "Bedsure 100% Cotton Percale Duvet Cover", url: "https://amzn.to/44fAaP3", img: "Bedsure 100_ Cotton Percale Duvet Cover.jpg" },
      { name: "AoraPulse Portable Foldable Treadmills", url: "https://amzn.to/3Sfz5UK", img: "AoraPulse Portable Foldable Treadmills.jpg" },
      { name: "Yankee Candle Sage & Citrus", url: "https://amzn.to/4eQ6iyI", img: "Yankee Candle Sage & Citrus.jpg" },
      { name: "Sweetcrispy Criss Cross Chair", url: "https://amzn.to/4oC8kG3", img: "Sweetcrispy Criss Cross Chair.jpg" },
      { name: "STANLEY Quencher H2.0 Tumbler", url: "https://amzn.to/4xSE9yT", img: "STANLEY Quencher H2.0 Tumbler.jpg" },
      { name: "STANLEY Quencher ProTour Flip Straw Tumbler", url: "https://amzn.to/3Sy3my9", img: "STANLEY Quencher ProTour Flip Straw Tumbler.jpg" },
      { name: "Chefman Air Fryer", url: "https://amzn.to/3QqSj9q", img: "Chefman Air Fryer.jpg" },
      { name: "Drinking Glasses with Bamboo Lids", url: "https://amzn.to/4xBWyQ3", img: "Drinking Glasses with Bamboo Lids.jpg" },
      { name: "Fullstar Vegetable Chopper & Mandoline", url: "https://amzn.to/4vAopit", img: "Fullstar Vegetable Chopper & Mandoline.jpg" }
    ]
  },
  {
    name: "Pride",
    items: [
      { name: "Nanafast Titanium Stainless Steel Rainbow LGBT Pride Bracelet", url: "https://amzn.to/4vh1SXz", img: "Nanafast Titanium Stainless Steel Rainbow LGBT Pride Bracelet.jpg" },
      { name: "YOU CAN BE YOURSELF WITH ME Enamel LGBT Lapel Pin", url: "https://amzn.to/4ef8bF4", img: "YOU CAN BE YOURSELF WITH ME Enamel LGBT Lapel Pin.jpg" },
      { name: "Rainbow Pride Baseball Hat", url: "https://amzn.to/3SMftrq", img: "Rainbow Pride Baseball Hat.jpg" },
      { name: "Double Sided Inclusive Progress Pride Rainbow Flag", url: "https://amzn.to/4ecl4Qg", img: "Double Sided Inclusive Progress Pride Rainbow Flag.jpg" },
      { name: "Small Gay Pride Stick Flags", url: "https://amzn.to/4eSMR7B", img: "Small Gay Pride Stick Flags.jpg" }
    ]
  },
  {
    name: "Pride Pops",
    items: [
      { name: "Funko Pop! Pride Extraño", url: "https://amzn.to/4fO97l3", img: "Funko Pop! Pride Extraño.jpg" },
      { name: "Funko Pop Heroes Pride Poison Ivy", url: "https://amzn.to/4ow9GlG", img: "Funko Pop! Pride Poison Ivy.jpg" },
      { name: "Funko Pop! Pride Batwoman", url: "https://amzn.to/43CLe8N", img: "Funko Pop! Pride Batwoman.jpg" },
      { name: "Funko Disney Pride Ursula", url: "https://amzn.to/4a1wuUA", img: "Funko Disney Pride Ursula.jpg" },
      { name: "Funko Pop! Heroes Pride Constantine", url: "https://amzn.to/43GrOzO", img: "Funko Pop! Heroes Pride Constantine.jpg" },
      { name: "Funko Pop! Heroes Pride Harley Quinn", url: "https://amzn.to/4xqUFWm", img: "Funko Pop! Heroes Pride Harley Quinn.jpg" },
      { name: "Funko DC Heroes Poison Ivy, Harley Quinn and Robin Rainbow 3-Pack", url: "https://amzn.to/4evjibM", img: "Funko DC Heroes Poison Ivy, Harley Quinn and Robin Rainbow 3-Pack.jpg" },
      { name: "Funko Pop Heroes Pride Robin", url: "https://amzn.to/4xBlhnK", img: "Funko Pop Heroes Pride Robin.jpg" },
      { name: "Funko POP Star Wars Pride Stormtrooper", url: "https://amzn.to/3Q952xv", img: "Funko POP Star Wars Pride Stormtrooper.jpg" },
      { name: "Funko POP Disney Pride Mickey Mouse", url: "https://amzn.to/43Isu7J", img: "Funko POP Disney Pride Mickey Mouse.jpg" },
      { name: "Funko POP Disney Pride Stitch", url: "https://amzn.to/4aWKXkS", img: "Funko POP Disney Pride Stitch.jpg" },
      { name: "Funko Pop! Sanrio Pride 2020 Hello Kitty", url: "https://amzn.to/44ci6W2", img: "Funko Pop! Sanrio Pride 2020 Hello Kitty.jpg" },
      { name: "Funko Pop! Pride 2020 Spongebob", url: "https://amzn.to/4vVJ9AW", img: "Funko Pop! Pride 2020 Spongebob.jpg" },
      { name: "Funko POP Animation Pride Tina Belcher", url: "https://amzn.to/3Qtds2z", img: "Funko POP Animation Pride Tina Belcher.jpg" }
    ]
  },
  {
    name: "Anime Pops",
    subcategories: [
      {
        name: "Solo Leveling",
        items: [
          { name: "Funko Pop! Animation Solo Leveling Sung Jinwoo", url: "https://amzn.to/4vh2Kvj", img: "Funko Pop! Animation Solo Leveling Sung Jinwoo.jpg" },
          { name: "Funko Pop! Animation Solo Leveling Yoo Jinho", url: "https://amzn.to/4uJfutB", img: "Funko Pop! Animation Solo Leveling Yoo Jinho.jpg" },
          { name: "Funko Pop! Animation Solo Leveling Choi Jong", url: "https://amzn.to/4oweVSl", img: "Funko Pop! Animation Solo Leveling Choi Jong.jpg" },
          { name: "Funko Pop! Animation Solo Leveling Woo Jinchul", url: "https://amzn.to/3QnynEs", img: "Funko Pop! Animation Solo Leveling Woo Jinchul.jpg" },
          { name: "Funko Pop! Animation Solo Leveling Go Gunhee", url: "https://amzn.to/4vVJymW", img: "Funko Pop! Animation Solo Leveling Go Gunhee.jpg" },
          { name: "Funko Pop! Animation Solo Leveling Igirs", url: "https://amzn.to/4vPXzST", img: "Funko Pop! Animation Solo Leveling Igirs.jpg" },
          { name: "Funko Pop! Animation Solo Leveling Cha Hae-in", url: "https://amzn.to/4fS4dDI", img: "Funko Pop! Animation Solo Leveling Cha Hae-in.jpg" },
          { name: "Funko Pop! Animation Solo Leveling Baek Yoonho", url: "https://amzn.to/4xFkpP6", img: "Funko Pop! Animation Solo Leveling Baek Yoonho.jpg" },
          { name: "Funko Pop! Animation Solo Leveling Woo Jinchu", url: "https://amzn.to/4uB1rWR", img: "Funko Pop! Animation Solo Leveling Woo Jinchu.jpg" },
          { name: "Funko Pop! Animation Solo Leveling Tank", url: "https://amzn.to/4oDxjcb", img: "Funko Pop! Animation Solo Leveling Tank.jpg" },
          { name: "Funko Pop! Animation Solo Leveling Sung Jinwoo Glows in The Dark", url: "https://amzn.to/4uO5XBz", img: "Funko Pop! Animation Solo Leveling Sung Jinwoo Glows in The Dark.jpg" },
          { name: "Funko Pop! Animation Solo Leveling Igris as Blood-Red Commander", url: "https://amzn.to/3QJLfEZ", img: "Funko Pop! Animation Solo Leveling Igris as Blood-Red Commander.jpg" }
        ]
      },
      {
        name: "Rezero",
        items: [
          { name: "Funko Pop! Animation Rezero Rem", url: "https://amzn.to/4vk5QyM", img: "Funko Pop! Animation Rezero Rem.jpg" },
          { name: "Funko Pop! Animation Re Zero Subaru Natsuki", url: "https://amzn.to/4a2W4Zo", img: "Funko Pop! Animation Re Zero Subaru Natsuki.jpg" },
          { name: "Funko Pop! Animation Re Zero Emilia with Puck", url: "https://amzn.to/3ScMBIN", img: "Funko Pop! Animation Re Zero Emilia with Puck.jpg" },
          { name: "Funko Pop! Animation Re Zero Ram", url: "https://amzn.to/43JHtyl", img: "Funko Pop! Animation Re Zero Ram.jpg" }
        ]
      },
      {
        name: "Jujutsu Kaisen",
        items: [
          { name: "Funko Pop! Jujutsu Kaisen Megumi Fushiguro with Dogs", url: "https://amzn.to/4vUlTTE", img: "Funko Pop! Jujutsu Kaisen Megumi Fushiguro with Dogs.jpg" },
          { name: "Funko POP! Animation JJK Ultimate Mechamaru", url: "https://amzn.to/3QbOBR0", img: "Funko POP! Animation JJK Ultimate Mechamaru.jpg" },
          { name: "Funko Pop! JJK Aoi Todo", url: "https://amzn.to/4owaI12", img: "Funko Pop! JJK Aoi Todo.jpg" },
          { name: "Funko POP! Animation Jujutsu Kaisen Sukuna", url: "https://amzn.to/4uO6jbn", img: "Funko POP! Animation Jujutsu Kaisen Sukuna.jpg" },
          { name: "Funko Pop! Animation Jujutsu Kaisen Yuji Itadori", url: "https://amzn.to/4uSwmyk", img: "Funko Pop! Animation Jujutsu Kaisen Yuji Itadori.jpg" },
          { name: "Funko Pop! Animation Jujitsu Kaisen Satoru Gojo", url: "https://amzn.to/4uIkuig", img: "Funko Pop! Animation Jujitsu Kaisen Satoru Gojo.jpg" },
          { name: "Funko Pop! Jujutsu Kaisen Nobara", url: "https://amzn.to/4eymp2Q", img: "Funko Pop! Jujutsu Kaisen Nobara.jpg" }
        ]
      }
    ]
  },
  {
    name: "Vinyl",
    items: [
      { name: "Bewitched - The Goddess Edition", url: "https://amzn.to/4ep64NO", img: "Bewitched - The Goddess Edition.jpg" },
      { name: "Taylor Swift The Tortured Poets Department The Anthology", url: "https://amzn.to/4w11MU5", img: "Taylor Swift The Tortured Poets Department The Anthology.jpg" },
      { name: "Taylor Swift Lover", url: "https://amzn.to/3ShhMTd", img: "Taylor Swift Lover.jpg" },
      { name: "Taylor Swift The Tortured Poets Department", url: "https://amzn.to/4uLaULA", img: "Taylor Swift The Tortured Poets Department.jpg" },
      { name: "Taylor Swift 1989 (Taylor's Version)", url: "https://amzn.to/4ePKeEs", img: "Taylor Swift 1989 (Taylor's Version).jpg" },
      { name: "Taylor Swift - 3  Vinyl Collection – Midnight Moonstone Blue Red", url: "https://amzn.to/4vWGaIl", img: "Taylor Swift - 3  Vinyl Collection – Midnight Moonstone Blue Red.jpg" },
      { name: "Taylor Swift The Life of a Showgirl", url: "https://amzn.to/3SetDl4", img: "Taylor Swift The Life of a Showgirl.jpg" },
      { name: "Pink Floyd The Dark Side of the Moon (50th Anniversary Remaster)", url: "https://amzn.to/4xzx7P1", img: "Pink Floyd The Dark Side of the Moon (50th Anniversary Remaster).jpg" },
      { name: "Minecraft Volume Alpha & Minecraft Volume Beta", url: "https://amzn.to/4uMtRgS", img: "Minecraft Volume Alpha & Minecraft Volume Beta.jpg" },
      { name: "Michael Jackson Thriller", url: "https://amzn.to/4fNrnuM", img: "Michael Jackson Thriller.jpg" }
    ]
  },
  {
    name: "Electronics",
    subcategories: [
      {
        name: "TV",
        items: [
          { name: "INSIGNIA 40 Inch Class FE Series LED Full HD Smart Fire TV", url: "https://amzn.to/4aESrZH", img: "INSIGNIA 40 Inch Class FE Series LED Full HD Smart Fire TV.jpg" },
          { name: "Amazon Ember 55 Inch Mini-LED Series with Fire TV", url: "https://amzn.to/4viLuWs", img: "Amazon Ember 55 Inch Mini-LED Series with Fire TV.jpg" },
          { name: "Amazon Ember 43 Inch 4K Ultra HD smart TV", url: "https://amzn.to/4a31jrV", img: "Amazon Ember 43 Inch 4K Ultra HD smart TV.jpg" },
          { name: "Amazon Ember 40 Inch 2-Series with Fire TV", url: "https://amzn.to/4xwjVe1", img: "Amazon Ember 40 Inch 2-Series with Fire TV.jpg" },
          { name: "INSIGNIA 50 Inch Class F50 Series LED 4K UHD Smart Fire TV", url: "https://amzn.to/4ef9kfQ", img: "INSIGNIA 50 Inch Class F50 Series LED 4K UHD Smart Fire TV.jpg" },
          { name: "INSIGNIA 32 Inch Class F20 Series LED HD Smart Fire TV", url: "https://amzn.to/4eSOd2b", img: "INSIGNIA 32 Inch Class F20 Series LED HD Smart Fire TV.jpg" }
        ]
      },
      {
        name: "Audio",
        items: [
          { name: "Sound Bar for Smart TV", url: "https://amzn.to/4ewGUgi", img: "Sound Bar for Smart TV.jpg" },
          { name: "ULTIMEA 7.1ch Surround Sound Bar", url: "https://amzn.to/4eq6Aej", img: "ULTIMEA 7.1ch Surround Sound Bar.jpg" },
          { name: "ULTIMEA Sound Bar with Wireless Subwoofer", url: "https://amzn.to/4vQr4E5", img: "ULTIMEA Sound Bar with Wireless Subwoofer.jpg" }
        ]
      },
      {
        name: "Gaming",
        items: [
          { name: "Fire TV Cube + Luna Controller", url: "https://amzn.to/4vjflOM", img: "Fire TV Cube + Luna Controller.jpg" },
          { name: "Luna Controller + FREE 1-month Luna Premium", url: "https://amzn.to/4ei4rmc", img: "Luna Controller + FREE 1-month Luna Premium.jpg" }
        ]
      }
    ]
  },
  {
    name: "Toiletries",
    items: [
      { name: "Striking Viking Vanilla Beard Oil for Men", url: "https://amzn.to/4xHI9lF", img: "Striking Viking Vanilla Beard Oil for Men.jpg" },
      { name: "Blackstone Men's Grooming Detoxifying Face Wash", url: "https://amzn.to/4gb2Yj9", img: "Blackstone Men's Grooming Detoxifying Face Wash.jpg" },
      { name: "hello Epic Whitening Charcoal Fluoride Free Toothpaste", url: "https://amzn.to/4eQbfaM", img: "hello Epic Whitening Charcoal Fluoride Free Toothpaste.jpg" },
      { name: "Fiber Lock Hair Spray by Minute Hair", url: "https://amzn.to/4xBZMD9", img: "Fiber Lock Hair Spray by Minute Hair.jpg" },
      { name: "e.l.f. Power Grip Dewy Setting Spray", url: "https://amzn.to/4uJi031", img: "e.l.f. Power Grip Dewy Setting Spray.jpg" },
      { name: "e.l.f. Hydrating Camo Concealer", url: "https://amzn.to/4v1Hp8t", img: "e.l.f. Hydrating Camo Concealer.jpg" },
      { name: "e.l.f. Camo Color Corrector", url: "https://amzn.to/4vkfWjd", img: "e.l.f. Camo Color Corrector.jpg" },
      { name: "Native Deodorant Coconut & Vanilla", url: "https://amzn.to/4a67H1F", img: "Native Deodorant Coconut & Vanilla.jpg" },
      { name: "Native Aluminum Free Deoderant Sea Salt & Cedar", url: "https://amzn.to/4xBOtej", img: "Native Aluminum Free Deoderant Sea Salt & Cedar.jpg" },
      { name: "Native Liquid Hand Soap Coconut & Vanilla", url: "https://amzn.to/4eq7Iyz", img: "Native Liquid Hand Soap Coconut & Vanilla.jpg" },
      { name: "Native Moisturizing Bodywash Cocoa Butter & Vanilla", url: "https://amzn.to/4w12kt7", img: "Native Moisturizing Bodywash Cocoa Butter & Vanilla.jpg" }
    ]
  }
];

// Map products from the category structure
const allProducts = ref<Product[]>([]);

const initializeProducts = () => {
  const initial: Product[] = [];
  categories.forEach(cat => {
    if (cat.items) {
      cat.items.forEach((item, idx) => {
        const id = `${cat.name.toLowerCase().replace(/\s+/g, '-')}-${idx + 1}`;
        initial.push({
          id,
          name: item.name,
          price: "Check Price",
          imageUrl: getImageUrl(item.img),
          amazonUrl: item.url,
          category: cat.name
        });
      });
    }
    if (cat.subcategories) {
      cat.subcategories.forEach(sub => {
        // @ts-ignore
        if (sub.items) {
          // @ts-ignore
          sub.items.forEach((item, idx) => {
            const id = `${sub.name.toLowerCase().replace(/\s+/g, '-')}-${idx + 1}`;
            initial.push({
              id,
              name: item.name,
              price: "Check Price",
              imageUrl: getImageUrl(item.img),
              amazonUrl: item.url,
              category: cat.name,
              subcategory: sub.name
            });
          });
        }
      });
    }
  });
  allProducts.value = initial;
};

initializeProducts();

const filteredProducts = computed(() => {
  if (activeCategory.value === 'All') return allProducts.value;
  return allProducts.value.filter(p => p.category === activeCategory.value);
});

// Group filtered products by subcategory if applicable
const groupedProducts = computed(() => {
  const groups: Record<string, Product[]> = {};
  filteredProducts.value.forEach(p => {
    const key = p.subcategory || 'General';
    if (!groups[key]) groups[key] = [];
    groups[key].push(p);
  });
  return groups;
});

const categoryList = ['All', ...categories.map(c => c.name)];
</script>

<template>
  <section id="shop" class="bg-zinc-900 py-20 px-6 min-h-screen">
    <div class="max-w-7xl mx-auto">
      <div class="text-center mb-16">
        <h2 class="text-4xl md:text-5xl font-black text-white uppercase italic tracking-tighter">
          The <span class="text-pink-500">Collection</span>
        </h2>
        <div class="h-1 w-20 bg-pink-500 mx-auto mt-4 rounded-full"></div>
        
        <!-- Category Filter -->
        <div class="mt-12 flex flex-wrap justify-center gap-4">
          <button 
            v-for="cat in categoryList" 
            :key="cat"
            @click="activeCategory = cat"
            :class="[
              'px-6 py-2 rounded-full font-bold uppercase tracking-widest text-[10px] transition-all duration-300 border',
              activeCategory === cat 
                ? 'bg-pink-500 border-pink-500 text-white shadow-lg shadow-pink-500/20' 
                : 'bg-transparent border-zinc-700 text-zinc-400 hover:border-pink-500/50 hover:text-white'
            ]"
          >
            {{ cat }}
          </button>
        </div>
      </div>

      <div v-for="(group, subcat) in groupedProducts" :key="subcat" class="mb-16">
        <h3 v-if="subcat !== 'General'" class="text-xl font-black text-white uppercase tracking-widest mb-8 border-l-4 border-pink-500 pl-4">
          {{ subcat }}
        </h3>
        
        <div class="grid grid-cols-1 sm:grid-cols-2 lg:grid-cols-3 xl:grid-cols-4 gap-6">
          <div 
            v-for="product in group" 
            :key="product.id"
            class="flex flex-col bg-zinc-800 rounded-2xl overflow-hidden border border-zinc-700 hover:border-pink-500/50 transition-all duration-300 group"
          >
            <div class="aspect-square overflow-hidden bg-zinc-700 relative">
              <img 
                :src="product.imageUrl" 
                :alt="product.name" 
                class="w-full h-full object-cover group-hover:scale-110 transition-transform duration-500"
              />
              <div v-if="product.subcategory" class="absolute top-4 left-4 bg-black/60 backdrop-blur-md text-white text-[9px] font-black uppercase px-2 py-1 rounded border border-white/10">
                {{ product.subcategory }}
              </div>
            </div>
            
            <div class="p-5 flex flex-col flex-grow space-y-3">
              <div class="flex justify-between items-start gap-2">
                <h4 class="text-base font-bold text-white line-clamp-2 leading-tight group-hover:text-pink-500 transition-colors">{{ product.name }}</h4>
                <span class="text-pink-500 font-black text-sm whitespace-nowrap">{{ product.price }}</span>
              </div>
              
              <div class="pt-2 mt-auto">
                <a 
                  :href="product.amazonUrl" 
                  target="_blank" 
                  rel="noopener noreferrer"
                  class="w-full py-2.5 bg-zinc-700 hover:bg-pink-600 text-white text-center font-bold text-xs rounded-xl transition-all border border-zinc-600 hover:border-pink-500 flex items-center justify-center gap-2 group/btn"
                >
                  View on Amazon
                  <svg xmlns="http://www.w3.org/2000/svg" class="w-3 h-3 group-hover/btn:translate-x-1 transition-transform" fill="none" viewBox="0 0 24 24" stroke="currentColor">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M14 5l7 7m0 0l-7 7m7-7H3" />
                  </svg>
                </a>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
