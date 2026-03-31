<script setup lang="ts">
import TopNavbar from '@/components/layout/TopNavbar.vue'
import AppFooter from '@/components/layout/AppFooter.vue'
import CornerBrackets from '@/components/ui/CornerBrackets.vue'
import DecryptedText from "@/components/ui/DecryptedText.vue";
import PixelWaveBackground from '@/components/ui/PixelWaveBackground.vue'
import image_os from "@/assets/projet_os.png"
import image_wiki from "@/assets/projet_wiki.jpg"
import image_design from "@/assets/projet_folio_design.png"

// Données des projets - Facile à mettre à jour
const projects = [
  {
    id: 'PHASE_01 // 2025',
    title: 'vabyzOS',
    image: image_os,
    tags: ['NIXOS', 'DOTFILE', 'NIX', 'DESIGN'],
    link:"https://github.com/vabyz971/vabyzOS"
  },
  {
    id: 'PHASE_02 // 2025',
    title: 'Carx Street',
    image: image_wiki,
    tags: ['WIKI', 'COMMUNAUTER'],
    link:"https://carxstreet.wiki.gg"
  },
  {
    id: 'PHASE_03 // 2025',
    title: 'PORTFOLIO Design',
    image: image_design,
    tags: ['ILLUSTRATOR', 'PHOTOPHOPE', 'INDESIGN'],
    link:"https://www.behance.net/gallery/242119957/PORTFOLIO-JL"
  }
]
</script>

<template>
  <div class="relative min-h-screen text-on-surface selection:bg-primary selection:text-on-primary overflow-x-hidden">
    
    <CornerBrackets />
    <TopNavbar />

    <div class="fixed inset-0 z-0 opacity-20 pointer-events-none">
      <div class="absolute inset-0 bg-gradient-to-b from-background via-transparent to-background z-10"></div>
      <PixelWaveBackground />
    </div>

    <div class="relative z-10">
      <main class="pt-32 pb-32 px-6 md:px-12 max-w-7xl mx-auto min-h-screen">
        
        <div class="mb-12 flex flex-col md:flex-row md:items-end justify-between gap-6">
          <div class="space-y-2">
            <div class="flex items-center gap-2">
              <span class="w-2 h-2 bg-primary"></span>
              <span class="font-label text-xs tracking-[0.3em] uppercase text-secondary font-bold"><DecryptedText text="BASE DE DONNÉES PROJETS" /></span>
            </div>
            <h1 class="font-headline text-5xl md:text-7xl font-bold uppercase tracking-tight max-w-3xl">PROJETS</h1>
          </div>
        </div>

        <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-1 p-1">
          <a 
            v-for="project in projects" 
            :key="project.title"
            :href="project.link"
            target="_blank"
            class="group relative bg-surface-container-low overflow-hidden transition-all duration-200 hover:z-10 cursor-pointer"
          >
            <div class="aspect-[16/10] overflow-hidden grayscale group-hover:grayscale-0 transition-all duration-500">
              <img 
                :src="project.image" 
                :alt="project.title"
                class="w-full h-full object-cover transform group-hover:scale-105 transition-transform duration-700"
              />
            </div>

            <div class="p-6 space-y-4 border-t border-outline-variant/10">
              <div class="flex justify-between items-start">
                <div>
                  <span class="font-label text-[10px] tracking-widest text-on-surface-variant uppercase block mb-1">{{ project.id }}</span>
                  <h3 class="font-headline text-xl font-bold uppercase tracking-tight group-hover:text-primary transition-colors">
                    {{ project.title }}
                  </h3>
                </div>
                <span class="material-symbols-outlined text-on-surface-variant group-hover:text-primary group-hover:translate-x-1 transition-all">
                  north_east
                </span>
              </div>
              
              <div class="flex gap-2">
                <span 
                  v-for="tag in project.tags" 
                  :key="tag"
                  class="text-[9px] font-label px-2 py-0.5 border border-outline-variant text-on-surface-variant uppercase"
                >
                  {{ tag }}
                </span>
              </div>
            </div>

            <div class="absolute top-0 left-0 w-2 h-2 border-t border-l border-primary opacity-0 group-hover:opacity-100 transition-opacity"></div>
            <div class="absolute bottom-0 right-0 w-2 h-2 border-b border-r border-primary opacity-0 group-hover:opacity-100 transition-opacity"></div>
        </a>
        </div>
      </main>

      <AppFooter />
    </div>
  </div>
</template>