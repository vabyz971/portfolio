<script setup lang="ts">
import { ref, watch, nextTick } from 'vue'
import { useRoute } from 'vue-router'
import DecryptedText from '@/components/ui/DecryptedText.vue'

const route = useRoute()
const latency = ref(0)
const isCalculating = ref(true)

watch(
  () => route.path,
  () => {
    isCalculating.value = true
    const startTime = performance.now()

    nextTick(() => {
      requestAnimationFrame(() => {
        const endTime = performance.now()
        
        let rawLatency = Math.round(endTime - startTime)
        latency.value = Math.max(1, rawLatency) 
        isCalculating.value = false
      })
    })
  },
  { immediate: true } 
)
</script>

<template>
  <footer class="fixed bottom-0 bg-[#0e0e0e] flex justify-between items-center w-full px-8 py-6 border-t border-[#1a1919] z-50">
    <div class="font-body text-[10px] tracking-[0.2em] uppercase text-white/40">
      © 2026 jahleel lacascade
    </div>
    
    <div class="flex gap-8 items-center">
      <span class="font-body text-[10px] tracking-[0.2em] uppercase text-[#F3FF00] flex items-center gap-2">
        <span class="w-1.5 h-1.5 bg-[#F3FF00] block animate-pulse"></span>
        Status: <DecryptedText text="Online" :speed="40" :reveal-delay="500" />
      </span>
      
      <span class="font-body text-[10px] tracking-[0.2em] uppercase text-white/40 hidden sm:inline transition-opacity duration-200" :class="{'opacity-50': isCalculating}">
        Latency: {{ isCalculating ? '--' : latency }}ms
      </span>
      
      <span class="font-body text-[10px] tracking-[0.2em] uppercase text-white/40 hidden sm:inline">
        Nodes: 04
      </span>
    </div>
  </footer>
</template>