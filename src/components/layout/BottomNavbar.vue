<script setup lang="ts">
import { useRoute } from "vue-router";
const route = useRoute();

const statusItems = [
  { label: "HOME", icon: "apps", path: "/" },
  { label: "ARCHIVE", icon: "database", path: "/archive" },
  { label: "SKILL", icon: "psychology_alt", path: "/skill" },
  { label: "CONTACT", icon: "mail", path: "/contact" },
];
</script>

<template>
  <nav
    class="md:hidden fixed bottom-0 left-0 w-full z-50 flex justify-between items-center border-t border-[#484847]/20 bg-[#0e0e0e]/80 backdrop-blur-md h-16 shadow-[0_-4px_24px_rgba(243,255,0,0.05)]"
  >
    <RouterLink
      v-for="link in statusItems"
      :to="link.path"
      :key="link.label"
      class="flex flex-col items-center justify-center flex-1 h-full transition-colors group"
      :class="
        route.path === link.path
          ? 'bg-[#F3FF00] text-black'
          : 'text-[#484847] hover:bg-[#1a1919] hover:text-[#ff51fa]'
      "
    >
      <span
        class="material-symbols-outlined text-2xl"
        :style="
          route.path === link.path ? 'font-variation-settings: \'FILL\' 1' : ''
        "
      >
        {{ link.icon }}
      </span>
      <span
        class="font-body text-[9px] tracking-widest font-bold uppercase mt-1"
      >
        {{ link.label }}
      </span>

      <div
        v-if="route.path === link.path"
        class="absolute top-0 w-full h-[2px] bg-black/20"
      ></div>
    </RouterLink>
  </nav>
</template>
