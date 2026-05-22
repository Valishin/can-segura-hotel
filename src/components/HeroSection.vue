<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const scrollToContact = () => document.getElementById('contacto')?.scrollIntoView({ behavior: 'smooth' })
const scrollToServicios = () => document.getElementById('servicios')?.scrollIntoView({ behavior: 'smooth' })

const images = [
  '/images/170728235.jpg',
  '/images/170728294.jpg',
  '/images/491442953_17845042593461946_6593210908200984637_n.jpg',
]

const current = ref(0)
const prev = ref<number | null>(null)
const transitioning = ref(false)
let timer: ReturnType<typeof setInterval>

const next = () => {
  if (transitioning.value) return
  transitioning.value = true
  prev.value = current.value
  current.value = (current.value + 1) % images.length
  setTimeout(() => { prev.value = null; transitioning.value = false }, 1200)
}

onMounted(() => { timer = setInterval(next, 6000) })
onUnmounted(() => clearInterval(timer))
</script>

<template>
  <section id="hero" class="hero">
    <div v-if="prev !== null" class="hero-bg hero-bg--out" :style="{ backgroundImage: `url('${images[prev]}')` }"></div>
    <div class="hero-bg hero-bg--in" :key="current" :style="{ backgroundImage: `url('${images[current]}')` }"></div>
    <div class="hero-overlay"></div>

    <div class="hero-dots">
      <button v-for="(_, i) in images" :key="i" :class="['dot', { active: i === current }]"
        @click="() => { prev = current; current = i }" :aria-label="`Imagen ${i + 1}`" />
    </div>

    <div class="hero-content container">
      <div class="hero-tag">
        <span class="tag-line"></span>
        Cataluña · Descanso · Gastronomía
        <span class="tag-line"></span>
      </div>

      <h1 class="hero-title">
        <em>Can Segura</em>
        <span>Hotel & Restaurant</span>
      </h1>

      <p class="hero-tagline">
        Un refugio de paz y buen gusto en el corazón<br />de la naturaleza catalana
      </p>

      <div class="hero-actions">
        <button class="btn-primary" @click="scrollToContact">Consultar disponibilidad</button>
        <button class="btn-ghost" @click="scrollToServicios">Nuestros servicios</button>
      </div>
    </div>

    <div class="hero-scroll-hint">
      <div class="scroll-line"></div>
      <span>Descubre más</span>
    </div>
  </section>
</template>

<style scoped>
.hero {
  position: relative;
  min-height: 100svh;
  display: flex;
  align-items: center;
  overflow: hidden;
}

.hero-bg {
  position: absolute;
  inset: 0;
  background-size: cover;
  background-position: center;
}
.hero-bg--in {
  z-index: 1;
  animation: heroFadeIn 1.2s ease forwards;
}
.hero-bg--out {
  z-index: 0;
  animation: heroFadeOut 1.2s ease forwards;
}

@keyframes heroFadeIn {
  from { opacity: 0; transform: scale(1.04); }
  to   { opacity: 1; transform: scale(1); }
}
@keyframes heroFadeOut {
  from { opacity: 1; }
  to   { opacity: 0; }
}

.hero-overlay {
  position: absolute;
  inset: 0;
  z-index: 2;
  background: linear-gradient(
    155deg,
    rgba(15, 12, 8, 0.65) 0%,
    rgba(15, 12, 8, 0.42) 55%,
    rgba(15, 12, 8, 0.75) 100%
  );
}

.hero-content {
  position: relative;
  z-index: 3;
  padding-top: 96px;
}

.hero-dots {
  position: absolute;
  bottom: 2.5rem;
  right: 2.5rem;
  z-index: 4;
  display: flex;
  gap: 0.5rem;
}
.dot {
  width: 6px; height: 6px;
  border-radius: 50%;
  background: rgba(255,255,255,0.35);
  transition: background 0.3s, transform 0.3s;
}
.dot.active {
  background: #fff;
  transform: scale(1.5);
}

.hero-tag {
  display: flex;
  align-items: center;
  gap: 1rem;
  font-size: 0.7rem;
  font-weight: 600;
  letter-spacing: 0.25em;
  text-transform: uppercase;
  color: rgba(255,255,255,0.75);
  margin-bottom: 1.75rem;
  animation: fadeUp 0.8s 0.2s both;
}
.tag-line {
  display: block;
  width: 32px; height: 1px;
  background: rgba(255,255,255,0.5);
}

.hero-title {
  font-family: var(--font-serif);
  line-height: 1;
  margin-bottom: 1.5rem;
  animation: fadeUp 0.8s 0.35s both;
}
.hero-title em {
  display: block;
  font-size: clamp(3.5rem, 9vw, 7rem);
  font-weight: 400;
  font-style: italic;
  color: #fff;
  letter-spacing: -0.01em;
}
.hero-title span {
  display: block;
  font-size: clamp(1rem, 2.5vw, 1.8rem);
  font-weight: 400;
  color: rgba(255,255,255,0.7);
  letter-spacing: 0.35em;
  text-transform: uppercase;
  margin-top: 0.5rem;
}

.hero-tagline {
  font-size: clamp(1rem, 1.8vw, 1.15rem);
  color: rgba(255,255,255,0.7);
  line-height: 1.7;
  max-width: 480px;
  margin-bottom: 2.5rem;
  animation: fadeUp 0.8s 0.5s both;
}

.hero-actions {
  display: flex;
  gap: 1rem;
  flex-wrap: wrap;
  animation: fadeUp 0.8s 0.65s both;
}

.btn-primary {
  font-size: 0.85rem;
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--accent-dark);
  background: #fff;
  padding: 0.9rem 2rem;
  border-radius: var(--radius-sm);
  transition: background var(--transition), transform 0.2s;
}
.btn-primary:hover {
  background: var(--bg-secondary);
  transform: translateY(-2px);
}

.btn-ghost {
  font-size: 0.85rem;
  font-weight: 500;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: #fff;
  border: 1px solid rgba(255,255,255,0.45);
  padding: 0.9rem 2rem;
  border-radius: var(--radius-sm);
  transition: border-color var(--transition), background var(--transition), transform 0.2s;
}
.btn-ghost:hover {
  border-color: rgba(255,255,255,0.8);
  background: rgba(255,255,255,0.1);
  transform: translateY(-2px);
}

.hero-scroll-hint {
  position: absolute;
  bottom: 2.5rem;
  left: 50%;
  transform: translateX(-50%);
  z-index: 4;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.5rem;
  animation: fadeUp 1s 1.2s both;
}
.scroll-line {
  width: 1px; height: 48px;
  background: linear-gradient(to bottom, transparent, rgba(255,255,255,0.6));
  animation: scrollPulse 2s infinite;
}
@keyframes scrollPulse {
  0%, 100% { opacity: 0.4; }
  50% { opacity: 1; }
}
.hero-scroll-hint span {
  font-size: 0.65rem;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: rgba(255,255,255,0.5);
}

@keyframes fadeUp {
  from { opacity: 0; transform: translateY(24px); }
  to   { opacity: 1; transform: translateY(0); }
}
</style>
