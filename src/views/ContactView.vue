<script setup lang="ts">
import { ref } from 'vue'
import TopNavbar from '@/components/layout/TopNavbar.vue'
import AppFooter from '@/components/layout/AppFooter.vue'
import CornerBrackets from '@/components/ui/CornerBrackets.vue'
import PixelWaveBackground from '@/components/ui/PixelWaveBackground.vue'
import DecryptedText from '@/components/ui/DecryptedText.vue'

// État du formulaire
const formStatus = ref<'IDLE' | 'TRANSMITTING' | 'SUCCESS'>('IDLE')
const formData = ref({
  name: '',
  channel: '',
  message: ''
})

const handleTransmission = () => {
  if (!formData.value.name || !formData.value.channel || !formData.value.message) return
  
  formStatus.value = 'TRANSMITTING'
  
  // Simulation de l'envoi (tu pourras brancher ton API ici plus tard)
  setTimeout(() => {
    formStatus.value = 'SUCCESS'
    formData.value = { name: '', channel: '', message: '' }
    
    // Reset après quelques secondes
    setTimeout(() => {
      formStatus.value = 'IDLE'
    }, 5000)
  }, 2000)
}

const communicationNodes = [
  { id: 'NODE_01', name: 'GITHUB', value: 'github.com/vabyz971', link: 'https://github.com/vabyz971', status: 'ACTIVE' },
  { id: 'NODE_02', name: 'MAIL', value: 'j.lacascade971@gmail.com', link: 'mailto:j.lacascade971@gmail.com', status: 'ROUTING' }
]
</script>

<template>
  <div class="relative min-h-screen text-on-surface selection:bg-primary selection:text-on-primary overflow-x-hidden">
    
    <CornerBrackets />
    <TopNavbar />

    <div class="fixed inset-0 z-0 pointer-events-none">
      <div class="absolute inset-0 bg-gradient-to-b from-background via-transparent to-background z-10"></div>
      <PixelWaveBackground />
    </div>

    <div class="relative z-10">
      <main class="pt-32 pb-32 px-6 md:px-12 max-w-7xl mx-auto min-h-screen flex flex-col">
        
        <header class="mb-16 md:mb-24 space-y-4">
          <div class="flex items-center gap-3">
            <span class="w-2 h-2 bg-secondary block animate-pulse"></span>
            <span class="font-label text-xs tracking-[0.3em] uppercase text-secondary">
              <DecryptedText text="CANAL DE LIAISON SÉCURISÉ" :speed="15" />
            </span>
          </div>
          <h1 class="font-headline text-5xl md:text-7xl font-bold uppercase tracking-tight max-w-3xl">
            <DecryptedText text="CONTACT." :speed="30" :reveal-delay="300" />
          </h1>
        </header>

        <div class="grid grid-cols-1 lg:grid-cols-12 gap-8 lg:gap-16 flex-grow">
          
          <div class="lg:col-span-7 bg-surface-container-low border border-outline-variant/20 p-6 md:p-8 relative group">
            <div class="absolute top-0 left-0 w-2 h-2 border-t border-l border-primary opacity-50"></div>
            <div class="absolute bottom-0 right-0 w-2 h-2 border-b border-r border-primary opacity-50"></div>

            <div class="flex justify-between items-end mb-8 border-b border-outline-variant/20 pb-4">
              <h2 class="font-headline text-2xl font-bold uppercase tracking-wide">Transmission Data</h2>
              <span class="font-label text-[10px] tracking-widest text-primary uppercase">
                <span v-if="formStatus === 'IDLE'">AWAITING INPUT</span>
                <span v-else-if="formStatus === 'TRANSMITTING'" class="animate-pulse">ENCRYPTING...</span>
                <span v-else class="text-tertiary">DELIVERED</span>
              </span>
            </div>

            <form @submit.prevent="handleTransmission" class="space-y-6">
              <div class="grid grid-cols-1 md:grid-cols-2 gap-6">
                <div class="space-y-2">
                  <label class="font-label text-[10px] tracking-widest text-on-surface-variant uppercase block">Opérateur ID (Nom)</label>
                  <input 
                    v-model="formData.name"
                    type="text" 
                    required
                    :disabled="formStatus !== 'IDLE'"
                    class="w-full bg-background border border-outline-variant/30 px-4 py-3 font-body text-sm focus:border-primary focus:outline-none focus:ring-1 focus:ring-primary/50 transition-all disabled:opacity-50"
                  />
                </div>
                <div class="space-y-2">
                  <label class="font-label text-[10px] tracking-widest text-on-surface-variant uppercase block">Retour Signal (Email)</label>
                  <input 
                    v-model="formData.channel"
                    type="email" 
                    required
                    :disabled="formStatus !== 'IDLE'"
                    class="w-full bg-background border border-outline-variant/30 px-4 py-3 font-body text-sm focus:border-primary focus:outline-none focus:ring-1 focus:ring-primary/50 transition-all disabled:opacity-50"
                  />
                </div>
              </div>

              <div class="space-y-2">
                <label class="font-label text-[10px] tracking-widest text-on-surface-variant uppercase block">Payload (Message)</label>
                <textarea 
                  v-model="formData.message"
                  required
                  rows="5"
                  :disabled="formStatus !== 'IDLE'"
                  class="w-full bg-background border border-outline-variant/30 px-4 py-3 font-body text-sm focus:border-primary focus:outline-none focus:ring-1 focus:ring-primary/50 transition-all resize-none disabled:opacity-50"
                ></textarea>
              </div>

              <div class="pt-4">
                <button 
                  type="submit" 
                  :disabled="formStatus !== 'IDLE'"
                  class="w-full group relative flex items-center justify-center gap-4 px-8 py-4 bg-primary text-on-primary font-headline font-bold uppercase tracking-widest transition-all disabled:bg-surface-container disabled:text-on-surface-variant hover:bg-primary-dim"
                >
                  <span v-if="formStatus === 'IDLE'">Exécuter Transmission</span>
                  <span v-else-if="formStatus === 'TRANSMITTING'">Cryptage en cours...</span>
                  <span v-else>Paquet Envoyé</span>
                  
                  <span v-if="formStatus === 'IDLE'" class="material-symbols-outlined group-hover:translate-x-1 transition-transform">send</span>
                  <span v-else-if="formStatus === 'TRANSMITTING'" class="material-symbols-outlined animate-spin">sync</span>
                  <span v-else class="material-symbols-outlined">check circle</span>
                </button>
              </div>
            </form>
          </div>

          <div class="lg:col-span-5 space-y-8">

            <div>
              <h3 class="font-headline text-sm font-bold uppercase tracking-widest text-on-surface-variant mb-4">Noeuds De Communication</h3>
              <div class="space-y-2">
                <a 
                  v-for="node in communicationNodes" 
                  :key="node.id" 
                  :href="node.link"
                  target="_blank"
                  class="group flex items-center justify-between p-4 bg-surface-container hover:bg-surface-container-high border border-transparent hover:border-outline-variant/30 transition-all cursor-pointer"
                >
                  <div class="flex items-center gap-4">
                    <span class="font-label text-[10px] tracking-widest text-on-surface-variant group-hover:text-primary transition-colors">{{ node.id }}</span>
                    <div>
                      <span class="block font-headline text-sm font-bold uppercase">{{ node.name }}</span>
                      <span class="block font-label text-[10px] tracking-widest text-on-surface-variant mt-1">{{ node.value }}</span>
                    </div>
                  </div>
                  <div class="flex items-center gap-2">
                    <span class="w-1.5 h-1.5 rounded-full" :class="node.status === 'ACTIVE' ? 'bg-primary animate-pulse' : 'bg-secondary'"></span>
                    <span class="material-symbols-outlined text-on-surface-variant group-hover:text-primary transition-colors">arrow_forward</span>
                  </div>
                </a>
              </div>
            </div>
          </div>
        </div>
      </main>

      <AppFooter />
    </div>
  </div>
</template>