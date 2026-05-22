<script setup lang="ts">
import { ref, onMounted } from 'vue'

const sectionRef = ref<HTMLElement | null>(null)
const lightboxSrc = ref<string | null>(null)

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      entries.forEach((e) => {
        if (e.isIntersecting) {
          e.target.querySelectorAll('.reveal').forEach((el) => el.classList.add('visible'))
          observer.unobserve(e.target)
        }
      })
    },
    { threshold: 0.1 }
  )
  if (sectionRef.value) observer.observe(sectionRef.value)
})

const photos = [
  { src: '/images/33348455.jpg', alt: 'Can Segura', span: 'wide' },
  { src: '/images/33348481.jpg', alt: 'Can Segura', span: 'tall' },
  { src: '/images/170728235.jpg', alt: 'Can Segura', span: '' },
  { src: '/images/170728294.jpg', alt: 'Can Segura', span: '' },
  { src: '/images/33348420.jpg', alt: 'Can Segura', span: '' },
  { src: '/images/33348428.jpg', alt: 'Can Segura', span: '' },
  { src: '/images/491442953_17845042593461946_6593210908200984637_n.jpg', alt: 'Can Segura', span: 'tall' },
  { src: '/images/33348430.jpg', alt: 'Can Segura', span: '' },
  { src: '/images/33348436.jpg', alt: 'Can Segura', span: '' },
  { src: '/images/491444150_17844934254461946_5165182295044683036_n.jpg', alt: 'Can Segura', span: 'wide' },
  { src: '/images/33348439.jpg', alt: 'Can Segura', span: '' },
  { src: '/images/33348449.jpg', alt: 'Can Segura', span: '' },
]

const openLightbox = (src: string) => { lightboxSrc.value = src }
const closeLightbox = () => { lightboxSrc.value = null }
</script>

<template>
  <section id="galeria" class="gallery" ref="sectionRef">
    <div class="container">
      <div class="gallery-header reveal">
        <span class="section-label">Galería</span>
        <h2 class="section-title">Un vistazo a <em>Can Segura</em></h2>
        <p class="section-subtitle">Espacios, rincones y momentos que definen nuestra manera de entender la hospitalidad.</p>
      </div>
    </div>

    <div class="gallery-grid container">
      <div
        v-for="(photo, i) in photos"
        :key="i"
        class="gallery-item reveal"
        :class="[`reveal-delay-${(i % 4) + 1}`, photo.span]"
        @click="openLightbox(photo.src)"
      >
        <img :src="photo.src" :alt="photo.alt" />
        <div class="gallery-overlay"><span>+</span></div>
      </div>
    </div>

    <Transition name="lightbox">
      <div v-if="lightboxSrc" class="lightbox" @click="closeLightbox">
        <button class="lightbox-close" @click="closeLightbox">✕</button>
        <img :src="lightboxSrc" alt="Foto ampliada" @click.stop />
      </div>
    </Transition>
  </section>
</template>

<style scoped>
.gallery {
  padding: 8rem 0;
  background: var(--bg-primary);
  position: relative;
}
.gallery::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 1px;
  background: linear-gradient(to right, transparent, var(--border-accent), transparent);
}

.gallery-header { margin-bottom: 3rem; }
.gallery-header em { color: var(--accent); font-style: italic; }
.gallery-header .section-subtitle { max-width: 480px; }

.gallery-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: 220px;
  gap: 0.75rem;
}

.gallery-item {
  position: relative;
  overflow: hidden;
  border-radius: var(--radius-md);
  cursor: pointer;
  background: var(--bg-secondary);
}
.gallery-item.wide { grid-column: span 2; }
.gallery-item.tall { grid-row: span 2; }

.gallery-item img {
  width: 100%; height: 100%;
  object-fit: cover;
  transition: transform 0.55s ease;
}
.gallery-item:hover img { transform: scale(1.07); }

.gallery-overlay {
  position: absolute;
  inset: 0;
  background: rgba(139, 115, 85, 0.4);
  display: flex;
  align-items: center;
  justify-content: center;
  opacity: 0;
  transition: opacity var(--transition);
}
.gallery-overlay span {
  font-size: 2.5rem;
  color: #fff;
  font-weight: 300;
  line-height: 1;
}
.gallery-item:hover .gallery-overlay { opacity: 1; }

.lightbox {
  position: fixed;
  inset: 0;
  z-index: 2000;
  background: rgba(28, 24, 20, 0.94);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  cursor: pointer;
}
.lightbox img {
  max-width: 90vw;
  max-height: 85vh;
  object-fit: contain;
  border-radius: var(--radius-md);
  box-shadow: 0 20px 80px rgba(0,0,0,0.4);
}
.lightbox-close {
  position: absolute;
  top: 1.5rem; right: 1.5rem;
  font-size: 1.1rem;
  color: #fff;
  background: rgba(255,255,255,0.15);
  width: 40px; height: 40px;
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  transition: background var(--transition);
}
.lightbox-close:hover { background: var(--accent); }

.lightbox-enter-active, .lightbox-leave-active { transition: opacity 0.3s ease; }
.lightbox-enter-from, .lightbox-leave-to { opacity: 0; }

@media (max-width: 900px) {
  .gallery-grid { grid-template-columns: repeat(2, 1fr); grid-auto-rows: 180px; }
}
@media (max-width: 500px) {
  .gallery-grid { grid-template-columns: 1fr; grid-auto-rows: 220px; }
  .gallery-item.wide, .gallery-item.tall { grid-column: auto; grid-row: auto; }
}
</style>
