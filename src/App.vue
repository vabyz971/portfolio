<script setup lang="ts">
import { ref, nextTick } from 'vue'
import { useRouter } from 'vue-router'

import TopNavbar from "@/components/layout/TopNavbar.vue";
import BottomNavbar from "@/components/layout/BottomNavbar.vue";
import SmokeTransition from "@/components/ui/SmokeTransition.vue";

const transitionRef = ref()
const router = useRouter()

router.beforeEach(async (_to, _from, next) => {
    if (transitionRef.value) {
        // 1. On lance la fumée
        await transitionRef.value.cover();
        // 2. Une fois que c'est noir, on autorise le changement de page
        next();
    } else {
        next();
    }
});

router.afterEach(async () => {
    if (transitionRef.value) {
        // 3. On attend que Vue ait réellement rendu la nouvelle page dans le DOM
        await nextTick();
        // 4. On retire la fumée
        await transitionRef.value.reveal();
    }
});

</script>

<template>
  <div class="bg-background text-on-surface min-h-screen font-body">
    <SmokeTransition ref="transitionRef" />
    <TopNavbar />
    <router-view/>
    <BottomNavbar />
  </div>
</template>

<style>
</style>
