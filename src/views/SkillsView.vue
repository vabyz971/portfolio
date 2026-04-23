<script setup lang="ts">
import TopNavbar from "@/components/layout/TopNavbar.vue";
import AppFooter from "@/components/layout/AppFooter.vue";
import CornerBrackets from "@/components/ui/CornerBrackets.vue";
import PixelWaveBackground from "@/components/ui/PixelWaveBackground.vue";
import DecryptedText from "@/components/ui/DecryptedText.vue";

const coreSkills = [
  { name: "Programation", level: 80 },
  { name: "Infographie", level: 66 },
  { name: "Maintenance matériel", level: 100 },
  { name: "Linux", level: 80 },
  { name: "Gestion de Déploiement", level: 50 },
];

const deploymentLogs = [
  {
    years: "2023 — 2024",
    role: "Technician informatique",
    company: "Raoul Georges Nicolo",
    desc: "Maintenance du parc informatique",
    tags: ["Active Directory", "Synologie", "GLPI"],
  },
  {
    years: "2021 — 2022",
    role: "Pentester",
    company: "Caierus",
    desc: "Réalisation d'audits de sécurité offensive pour intrusion, Création d'outils d'audits",
    tags: ["Python", "Pentest", "Kali"],
  },
  {
    years: "2019 — 2020",
    role: "Développeur Web",
    company: "IPEOS",
    desc: "Conception de modules pour le framework Django",
    tags: ["Django", "Unifi"],
  },
];

const academicLogs = [
  {
    years: "2025 — 2026",
    degree: "DEP",
    school: "Bel-Avenir",
    desc: "DEP (Diplôme d'études professionnelles) en Infographie",
    tags: ["DEP +1"],
  },
  {
    years: "2020 — 2021",
    degree: "Licence CDA",
    school: "FORE ALTERNANCE",
    desc: "Licence CDA (Concepteur développeur D’application)",
    tags: ["Licence +1"],
  },
  {
    years: "2019 — 2020",
    degree: "Licence MIAGE",
    school: "Université des Antilles",
    desc: "Licence MIAGE (Méthode Informatique Appliquer à la Gestion D’entreprise)",
    tags: ["Licence +1"],
  },
  {
    years: "2017 — 2019",
    degree: "BTS (SIO) Services Informatiques aux Organisations",
    school: "Les Persévérants",
    desc: "Option SLAM (Solutions Logicielles et Applications Métiers). Focus sur le développement sécurisé et l'architecture réseau.",
    tags: ["Bac +2"],
  },
];
</script>

<template>
  <div
    class="relative min-h-screen bg-background text-on-surface selection:bg-primary selection:text-on-primary overflow-x-hidden"
  >
    <div class="fixed inset-0 z-0 opacity-20 pointer-events-none">
      <div
        class="absolute inset-0 bg-gradient-to-b from-background via-transparent to-background z-10"
      ></div>
      <PixelWaveBackground />
    </div>
    <div class="relative z-10">
      <CornerBrackets />
      <TopNavbar />

      <main
        class="relative pt-32 pb-32 px-6 md:px-12 lg:px-24 max-w-7xl mx-auto"
      >
        <header class="mb-20 space-y-4">
          <div class="flex items-center gap-3">
            <span class="w-2 h-2 bg-primary"></span>
            <span
              class="font-label text-xs font-bold tracking-[0.3em] uppercase text-secondary"
              ><DecryptedText text="Vue d'Ensemble Opérationnelle"/></span>
          </div>
          <h1
            class="font-headline text-5xl md:text-7xl font-bold uppercase tracking-tight max-w-3xl"
          >
            Compétences & <br />
            Expérience
          </h1>
          <p
            class="font-body text-on-surface-variant max-w-xl text-lg leading-relaxed"
          >
            Télémétrie des compétences techniques et expérience chronologique
            des engagements. Vérifié et mis à jour en temps réel.
          </p>
        </header>

        <section
          class="grid grid-cols-1 md:grid-cols-12 gap-1 mb-32 bg-surface-container-low p-1 border border-outline-variant/10"
        >
          <div class="md:col-span-7 bg-background p-8">
            <div class="flex justify-between items-end mb-12">
              <h2
                class="font-headline text-2xl font-bold uppercase tracking-wide"
              >
                Compétences Fondamentales
              </h2>
              <span
                class="font-label text-[10px] tracking-widest text-on-surface-variant uppercase"
                ><DecryptedText text="Mise à jour : 2026.03.30"/></span
              >
            </div>
            <div class="space-y-10">
              <div v-for="skill in coreSkills" :key="skill.name" class="group">
                <div class="flex justify-between mb-3 items-baseline">
                  <span
                    class="font-headline text-sm tracking-widest uppercase"
                    >{{ skill.name }}</span
                  >
                  <span class="font-label text-xs text-primary"
                    >{{ skill.level }}%</span
                  >
                </div>
                <div class="h-1.5 w-full bg-surface-container-highest">
                  <div
                    class="h-full bg-primary transition-all duration-1000"
                    :style="{ width: skill.level + '%' }"
                  ></div>
                </div>
              </div>
            </div>
          </div>

          <div
            class="md:col-span-5 bg-background p-8 flex flex-col justify-start border-l border-outline-variant/10"
          >
            <h3
              class="font-headline text-sm font-bold uppercase tracking-widest text-on-surface-variant mb-8"
            >
              Distribution des Nœuds
            </h3>
            <div
              class="aspect-square relative flex items-center justify-center border border-outline-variant/10"
            >
              <div
                class="absolute inset-0 opacity-10"
                style="
                  background-image: radial-gradient(
                    circle,
                    #fbffab 1px,
                    transparent 1px
                  );
                  background-size: 20px 20px;
                "
              ></div>
              <div class="z-10 text-center">
                <span
                  class="block font-headline text-6xl font-black text-primary mb-2"
                  >{{ coreSkills.length }}</span
                >
                <span
                  class="block font-label text-[10px] tracking-[0.4em] uppercase text-on-surface-variant"
                  ><DecryptedText text="Secteurs Globaux"/></span
                >
              </div>
              <div
                class="absolute top-0 left-0 w-4 h-4 border-t border-l border-primary/40"
              ></div>
              <div
                class="absolute bottom-0 right-0 w-4 h-4 border-b border-r border-primary/40"
              ></div>
            </div>
          </div>
        </section>

        <section class="space-y-12">
          <div
            class="flex items-center justify-between border-b border-outline-variant/20 pb-6"
          >
            <h2
              class="font-headline text-3xl font-bold uppercase tracking-tighter"
            >
              Log Experiences
            </h2>
            <div
              class="hidden md:block font-label text-[10px] tracking-widest text-on-surface-variant uppercase"
            >
              ID_Séquence : 9920-ALPHA
            </div>
          </div>

          <div
            v-for="log in deploymentLogs"
            :key="log.role"
            class="group grid grid-cols-1 md:grid-cols-12 py-12 border-b border-outline-variant/10 hover:bg-surface-container-low transition-colors px-4 -mx-4"
          >
            <div class="md:col-span-2 mb-4 md:mb-0">
              <span class="font-headline text-xl font-bold text-primary">{{
                log.years
              }}</span>
            </div>
            <div class="md:col-span-6 space-y-4">
              <div>
                <h3 class="font-headline text-2xl font-bold uppercase">
                  {{ log.role }}
                </h3>
                <p
                  class="font-label text-sm tracking-widest text-secondary mt-1 uppercase"
                >
                  {{ log.company }}
                </p>
              </div>
              <p
                class="font-body text-on-surface-variant max-w-lg leading-relaxed"
              >
                {{ log.desc }}
              </p>
            </div>
            <div
              class="md:col-span-4 flex flex-wrap gap-2 items-start justify-end"
            >
              <span
                v-for="tag in log.tags"
                :key="tag"
                class="bg-surface-container-highest border border-outline-variant/20 px-3 py-1 text-[10px] font-label uppercase tracking-widest text-on-surface-variant"
              >
                {{ tag }}
              </span>
            </div>
          </div>
        </section>

        <section class="space-y-12 mt-32">
          <div
            class="flex items-center justify-between border-b border-outline-variant/20 pb-6"
          >
            <h2
              class="font-headline text-3xl font-bold uppercase tracking-tighter"
            >
              Archives Académiques
            </h2>
            <div
              class="hidden md:block font-label text-[10px] tracking-widest text-on-surface-variant uppercase"
            >
              ID_Séquence : 8840-BETA
            </div>
          </div>

          <div
            v-for="edu in academicLogs"
            :key="edu.degree"
            class="group grid grid-cols-1 md:grid-cols-12 py-12 border-b border-outline-variant/10 hover:bg-surface-container-low transition-colors px-4 -mx-4"
          >
            <div class="md:col-span-2 mb-4 md:mb-0">
              <span class="font-headline text-xl font-bold text-primary">{{
                edu.years
              }}</span>
            </div>

            <div class="md:col-span-6 space-y-4">
              <div>
                <h3 class="font-headline text-2xl font-bold uppercase">
                  {{ edu.degree }}
                </h3>
                <p
                  class="font-label text-sm tracking-widest text-secondary mt-1 uppercase"
                >
                  {{ edu.school }}
                </p>
              </div>
              <p
                class="font-body text-on-surface-variant max-w-lg leading-relaxed"
              >
                {{ edu.desc }}
              </p>
            </div>

            <div
              class="md:col-span-4 flex flex-wrap gap-2 items-start justify-end"
            >
              <span
                v-for="tag in edu.tags"
                :key="tag"
                class="bg-surface-container-highest border border-outline-variant/20 px-3 py-1 text-[10px] font-label uppercase tracking-widest text-on-surface-variant"
              >
                {{ tag }}
              </span>
            </div>
          </div>
        </section>
      </main>
    </div>
    <AppFooter />
  </div>
</template>
