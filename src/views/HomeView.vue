<script setup lang="ts">
import HeroCore from "@/components/sections/HeroCore.vue";
import TopNavbar from "@/components/layout/TopNavbar.vue";
import AppFooter from "@/components/layout/AppFooter.vue";
import CornerBrackets from "@/components/ui/CornerBrackets.vue";
import PixelWaveBackground from "@/components/ui/PixelWaveBackground.vue";
</script>

<template>
  <div class="relative min-h-screen flex flex-col items-center justify-center text-on-surface selection:bg-primary selection:text-on-primary">
    
    <div class="fixed inset-0 z-0 opacity-50 pointer-events-none">
      <div class="absolute inset-0 bg-gradient-to-b from-background via-transparent to-background z-10"></div>
      <PixelWaveBackground />
    </div>

    <div class="relative z-10 w-full flex flex-col items-center justify-center">
      <CornerBrackets />
      <TopNavbar />

      <main class="relative w-full flex flex-col items-center justify-center px-6 pt-20 pb-24">
        <HeroCore />
      </main>

      <AppFooter />
    </div>
  </div>
</template>