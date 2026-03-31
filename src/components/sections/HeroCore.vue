<script setup lang="ts">
import DecryptedText from "@/components/ui/DecryptedText.vue";
</script>
<template>
  <section class="max-w-4xl w-full text-center space-y-12">
    <div
      class="font-mono text-primary/40 text-[10px] leading-tight mb-4 select-none"
    >
      //
      _________________________________________________________________________<br />
      // [SYSTEM_INIT_PHASE_01]
      ——————————————————————————————————————————————————
    </div>

    <div class="space-y-4">
      <h2
        class="font-label text-secondary text-sm tracking-[0.5em] uppercase font-bold"
      >
        <DecryptedText text="Identity Confirmed" />
      </h2>
      <h1
        class="font-headline text-7xl md:text-9xl font-black tracking-tighter text-on-surface uppercase leading-none"
      >
        JAHLEEL LACASCADE
      </h1>
      <p class="font-mono text-on-surface-variant text-lg leading-relaxed">
        Grand passionné d’open source, toujours en quête d’apprentissage.
      </p>
    </div>

    <div
      class="flex flex-col md:flex-row items-center justify-center gap-6 mt-16"
    >
      <RouterLink
        to="/archive"
        class="group relative px-10 py-5 border-2 border-outline-variant bg-transparent text-on-surface font-headline font-bold uppercase tracking-widest text-lg w-full md:w-auto transition-all active:translate-x-1 duration-75"
      >
        <span class="relative z-10 flex items-center justify-center gap-3">
          archive
          <span class="material-symbols-outlined text-2xl">database</span>
        </span>
        <div
          class="absolute inset-0 bg-on-surface/5 opacity-0 group-hover:opacity-100 transition-opacity"
        ></div>
      </RouterLink>

      <RouterLink
        to="/skill"
        class="group relative px-10 py-5 border-2 border-outline-variant bg-transparent text-on-surface font-headline font-bold uppercase tracking-widest text-lg w-full md:w-auto transition-all active:translate-x-1 duration-75"
      >
        <span class="relative z-10 flex items-center justify-center gap-3">
          SKILL
          <span class="material-symbols-outlined text-2xl">terminal</span>
        </span>
        <div
          class="absolute inset-0 bg-on-surface/5 opacity-0 group-hover:opacity-100 transition-opacity"
        ></div>
      </RouterLink>
    </div>

    <div class="flex justify-center items-center gap-12 pt-16">
      <div class="flex flex-col items-center">
        <span
          class="font-label text-[10px] text-on-surface-variant uppercase tracking-widest mb-2"
          >Sync Status</span
        >
        <div class="flex gap-1">
          <div class="w-3 h-1 bg-secondary"></div>
          <div class="w-3 h-1 bg-secondary"></div>
          <div class="w-3 h-1 bg-secondary"></div>
          <div class="w-3 h-1 bg-secondary"></div>
          <div class="w-3 h-1 bg-surface-container-highest"></div>
        </div>
      </div>
      <div class="flex flex-col items-center">
        <span
          class="font-label text-[10px] text-on-surface-variant uppercase tracking-widest mb-2"
          >Uptime</span
        >
        <span class="font-label text-xs text-primary tracking-widest"
          ><DecryptedText text="99.98% " /></span
        >
      </div>
      <div class="flex flex-col items-center">
        <span
          class="font-label text-[10px] text-on-surface-variant uppercase tracking-widest mb-2"
          >Node</span
        >
        <span class="font-label text-xs text-tertiary tracking-widest"
          ><DecryptedText text="CANADA" /></span
        >
      </div>
    </div>
  </section>
</template>
