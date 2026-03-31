<script setup lang="ts">
import { ref, onMounted } from 'vue';
import { Renderer, Geometry, Program, Mesh } from 'ogl';
import gsap from 'gsap';

const container = ref<HTMLElement | null>(null);
const isVisible = ref(false); 
let renderer: Renderer, gl: any, program: Program;

const vertex = `
    attribute vec2 position;
    attribute vec2 uv;
    varying vec2 vUv;
    void main() {
        vUv = uv;
        gl_Position = vec4(position, 0, 1);
    }
`;

const fragment = `
    precision highp float;
    uniform float uTime;
    uniform float uProgress;
    varying vec2 vUv;

    float hash(vec2 p) { return fract(sin(dot(p, vec2(127.1, 311.7))) * 43758.5453123); }
    float noise(vec2 p) {
        vec2 i = floor(p); vec2 f = fract(p);
        vec2 u = f * f * (3.0 - 2.0 * f);
        return mix(mix(hash(i + vec2(0,0)), hash(i + vec2(1,0)), u.x),
                   mix(hash(i + vec2(0,1)), hash(i + vec2(1,1)), u.x), u.y);
    }

    float fbm(vec2 p) {
        float v = 0.0; float a = 0.5;
        for (int i = 0; i < 5; i++) {
            v += a * noise(p); p *= 2.0; a *= 0.5;
        }
        return v;
    }

    void main() {
        vec2 uv = vUv;
        // n génère la distorsion de la fumée
        float n = fbm(uv * 2.5 + uTime * 0.4);
        float y = uv.y + n * 0.2;
        
        // La logique est séparée en deux "vagues" qui descendent.
        // bottom_edge = Le bas de la fumée (envahit l'écran)
        // top_edge = Le haut de la fumée (quitte l'écran)
        float bottom_edge = 1.5 - clamp(uProgress, 0.0, 1.0) * 1.8;
        float top_edge = 1.5 - clamp(uProgress - 1.0, 0.0, 1.0) * 1.8;
        
        // On calcule l'opacité en fonction des bordures
        float alphaBottom = smoothstep(bottom_edge - 0.4, bottom_edge, y);
        float alphaTop = 1.0 - smoothstep(top_edge - 0.4, top_edge, y);
        
        // La transparence finale est l'intersection des deux
        float finalAlpha = min(alphaBottom, alphaTop);

        // Couleur : noir très profond
        gl_FragColor = vec4(vec3(0.03), finalAlpha);
    }
`;

const initWebGL = () => {
    if (!container.value) return;

    renderer = new Renderer({ alpha: true });
    gl = renderer.gl;
    container.value.appendChild(gl.canvas);
    
    const geometry = new Geometry(gl, {
        position: { size: 2, data: new Float32Array([-1, -1, 3, -1, -1, 3]) },
        uv: { size: 2, data: new Float32Array([0, 0, 2, 0, 0, 2]) },
    });
    
    program = new Program(gl, {
        vertex, fragment,
        uniforms: { uTime: { value: 0 }, uProgress: { value: 0 } },
        transparent: true,
    });
    
    const mesh = new Mesh(gl, { geometry, program });
    
    const resize = () => renderer.setSize(window.innerWidth, window.innerHeight);
    window.addEventListener('resize', resize);
    resize();
    
    const update = (t: number) => {
        requestAnimationFrame(update);
        program.uniforms.uTime.value = t * 0.001;
        renderer.render({ scene: mesh });
    };
    requestAnimationFrame(update);
};

const cover = () => {
    isVisible.value = true;
    program.uniforms.uProgress.value = 0; 
    
    return gsap.to(program.uniforms.uProgress, {
        value: 1,
        duration: .8,
        ease: "power2.inOut"
    });
};

const reveal = () => {
    return gsap.to(program.uniforms.uProgress, {
        value: 2,
        duration: .8,
        ease: "power2.inOut",
        onComplete: () => {
            isVisible.value = false;
            program.uniforms.uProgress.value = 0;
        }
    });
};

onMounted(initWebGL);
defineExpose({ cover, reveal });
</script>

<template>
    <div 
        v-show="isVisible" 
        ref="container" 
        class="fixed inset-0 z-[600] pointer-events-none"
    ></div>
</template>