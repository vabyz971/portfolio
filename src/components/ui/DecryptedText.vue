<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';

// On définit les propriétés que le composant peut recevoir
const props = defineProps({
  text: {
    type: String,
    required: true
  },
  speed: {
    type: Number,
    default: 30 // Vitesse de rafraîchissement (ms)
  },
  revealDelay: {
    type: Number,
    default: 0 // Délai avant le début du décryptage
  }
});

const displayText = ref(props.text); // Par défaut, on affiche le texte complet (pour le SEO/fallback)
const spanRef = ref<HTMLSpanElement | null>(null);

const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789@#$%^&*_+-=;:,.<>?';
let intervalId: ReturnType<typeof setInterval>;
let observer: IntersectionObserver;

const startDecrypt = () => {
  let iteration = 0;
  clearInterval(intervalId);

  // Petite pause avant de commencer si revealDelay est défini
  setTimeout(() => {
    intervalId = setInterval(() => {
      displayText.value = props.text
        .split('')
        .map((letter, index) => {
          // On ne crypte pas les espaces
          if (letter === ' ') return ' ';
          
          // Si l'index est inférieur à l'itération actuelle, on affiche la vraie lettre
          if (index < iteration) {
            return props.text[index];
          }
          
          // Sinon, on affiche un caractère aléatoire
          return chars[Math.floor(Math.random() * chars.length)];
        })
        .join('');

      // On augmente doucement l'itération (fraction pour faire durer le glitch par lettre)
      iteration += 1 / 3;

      // Quand on a révélé tout le texte, on arrête l'intervalle
      if (iteration >= props.text.length) {
        clearInterval(intervalId);
        displayText.value = props.text;
      }
    }, props.speed);
  }, props.revealDelay);
};

onMounted(() => {
  // L'Intersection Observer permet de ne lancer l'effet QUE quand le texte apparaît à l'écran
  observer = new IntersectionObserver(
    (entries) => {
      if (entries[0].isIntersecting) {
        startDecrypt();
        // Une fois joué, on arrête d'observer pour ne pas le rejouer en boucle
        if (spanRef.value) observer.unobserve(spanRef.value);
      }
    },
    { threshold: 0.1 }
  );

  if (spanRef.value) {
    // Initialiser le texte avec des caractères cryptés avant même l'animation
    displayText.value = props.text.replace(/[^\s]/g, () => chars[Math.floor(Math.random() * chars.length)]);
    observer.observe(spanRef.value);
  }
});

onUnmounted(() => {
  clearInterval(intervalId);
  if (observer) observer.disconnect();
});
</script>

<template>
  <span ref="spanRef" class="font-mono inline-block">
    {{ displayText }}
  </span>
</template>