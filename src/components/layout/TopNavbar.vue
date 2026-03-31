<script setup lang="ts">
import { useRoute } from 'vue-router';

const route = useRoute();

const navLinks = [
  { name: "HOME", path: "/" },
  { name: "ARCHIVE", path: "/archive" },
  { name: "SKILL", path: "/skill" },
  { name: "CONTACT", path: "/contact" },
];
</script>

<template>
  <header
    class="fixed top-0 bg-[#0e0e0e] flex justify-between items-center w-full px-6 py-4 z-50 border-b border-outline-variant/10"
  >
    <div
      class="text-2xl font-black tracking-tighter text-[#F3FF00] font-headline uppercase"
    >
      PORTFOLIO
    </div>

    <nav class="hidden md:flex gap-8 items-center">
      <RouterLink
        v-for="link in navLinks"
        :to="link.path"
        :key="link.name"
        class="font-headline uppercase tracking-widest text-sm transition-colors duration-200"
        :class="route.path === link.path ? 'text-[#F3FF00]' : 'text-white/60 hover:text-white'"
      >
        / {{ link.name }}
      </RouterLink>
    </nav>

  </header>
</template>