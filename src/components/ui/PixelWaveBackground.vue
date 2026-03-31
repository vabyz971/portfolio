<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue';

const canvasRef = ref<HTMLCanvasElement | null>(null);
let animationId: number;
let resizeHandler: () => void;
let mouseMoveHandler: (e: MouseEvent) => void;
let touchMoveHandler: (e: TouchEvent) => void;

onMounted(() => {
  const canvas = canvasRef.value;
  if (!canvas) return;
  const ctx = canvas.getContext('2d');
  if (!ctx) return;

  const fontSize = 14;
  const chars = 'ABCDEFGHIJKLMNOPQRSTUVWXYZ0123456789@#$%^&*()_+-=[]{}|;:,.<>?'.split('');

  let cols = 0;
  let rows = 0;
  
  // Tableaux pour stocker l'état de chaque caractère
  let gridChars: string[][] = [];
  let gridOpacities: number[][] = [];

  // Suivi de la souris (avec une interpolation pour la fluidité)
  let mouseX = -1000;
  let mouseY = -1000;
  let targetMouseX = -1000;
  let targetMouseY = -1000;
  
  // Compteur d'images pour l'effet glitch
  let glitchFrames = 0;

  resizeHandler = () => {
    canvas.width = window.innerWidth;
    canvas.height = window.innerHeight;

    cols = Math.ceil(canvas.width / fontSize);
    rows = Math.ceil(canvas.height / fontSize);

    // Initialisation de la grille
    gridChars = Array(cols).fill(0).map(() =>
      Array(rows).fill(0).map(() => chars[Math.floor(Math.random() * chars.length)])
    );
    gridOpacities = Array(cols).fill(0).map(() => Array(rows).fill(0));
  };

  window.addEventListener('resize', resizeHandler);
  resizeHandler();

  // --- ÉVÉNEMENTS SOURIS & TACTILE ---
  mouseMoveHandler = (e: MouseEvent) => {
    targetMouseX = e.clientX;
    targetMouseY = e.clientY;
  };


  touchMoveHandler = (e: TouchEvent) => {
    targetMouseX = e.touches[0].clientX;
    targetMouseY = e.touches[0].clientY;
  };

  window.addEventListener('mousemove', mouseMoveHandler);
  window.addEventListener('touchmove', touchMoveHandler);

  const draw = () => {
    animationId = requestAnimationFrame(draw);

    mouseX += (targetMouseX - mouseX) * 0.2;
    mouseY += (targetMouseY - mouseY) * 0.2;

    ctx.clearRect(0, 0, canvas.width, canvas.height);

    ctx.font = `500 ${fontSize}px "Space Grotesk", monospace`;
    ctx.textAlign = 'center';
    ctx.textBaseline = 'middle';

    // Le rayon de lumière s'agrandit violemment pendant le glitch
    const radius = glitchFrames > 0 ? 300 : 120;

    for (let x = 0; x < cols; x++) {
      for (let y = 0; y < rows; y++) {
        const cellX = x * fontSize + fontSize / 2;
        const cellY = y * fontSize + fontSize / 2;

        // Calcul de la distance entre le curseur et la cellule
        const dx = mouseX - cellX;
        const dy = mouseY - cellY;
        const dist = Math.sqrt(dx * dx + dy * dy);

        // 1. Illumination si on est dans le rayon de la souris
        if (dist < radius) {
          const boost = 1 - (dist / radius);
          // On augmente l'opacité
          gridOpacities[x][y] = Math.max(gridOpacities[x][y], boost);
        }

        // 2. Dissipation lente (effet de traînée quand la souris part)
        gridOpacities[x][y] *= 0.90; // Réduit l'opacité de 10% à chaque frame

        // 3. Logique du Glitch (au clic)
        let isGlitchingCell = false;
        if (glitchFrames > 0) {
          // 40% de chance qu'une lettre change frénétiquement
          if (Math.random() < 0.4) {
            gridChars[x][y] = chars[Math.floor(Math.random() * chars.length)];
            isGlitchingCell = true;
          }
        } else {
          // Mutation naturelle très lente (pour que le fond ne soit pas figé)
          if (Math.random() < 0.0005) {
            gridChars[x][y] = chars[Math.floor(Math.random() * chars.length)];
          }
        }

        // 4. Rendu
        // On laisse une très légère opacité de base (0.02) pour qu'on devine la grille dans le noir
        const baseOpacity = 0.02; 
        const finalOpacity = Math.max(baseOpacity, gridOpacities[x][y]);

        if (finalOpacity > 0.01) {
          // Tremblement de la lettre pendant le glitch
          const offsetX = isGlitchingCell ? (Math.random() - 0.5) * 8 : 0;
          const offsetY = isGlitchingCell ? (Math.random() - 0.5) * 8 : 0;

          // Couleur Tactical (Jaune fluo), avec des flashs blancs pendant le glitch
          if (isGlitchingCell && Math.random() < 0.2) {
            ctx.fillStyle = `rgba(255, 255, 255, ${finalOpacity})`; // Flash blanc
          } else {
            ctx.fillStyle = `rgba(251, 255, 171, ${finalOpacity})`; // Jaune normal
          }

          ctx.fillText(gridChars[x][y], cellX + offsetX, cellY + offsetY);
        }
      }
    }

    // Réduction du timer de glitch
    if (glitchFrames > 0) glitchFrames--;
  };

  animationId = requestAnimationFrame(draw);
});

onBeforeUnmount(() => {
  window.removeEventListener('resize', resizeHandler);
  window.removeEventListener('mousemove', mouseMoveHandler);
  window.removeEventListener('touchmove', touchMoveHandler);
  cancelAnimationFrame(animationId);
});
</script>

<template>
  <canvas ref="canvasRef" class="w-full h-full block pointer-events-none opacity-80"></canvas>
</template>