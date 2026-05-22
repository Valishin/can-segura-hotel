<script setup lang="ts">
import { ref, onMounted } from 'vue'

const sectionRef = ref<HTMLElement | null>(null)

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

const services = [
  {
    name: 'Habitación Doble',
    description: 'Amplia habitación con vistas al jardín o a la montaña, baño privado, ropa de cama artesanal y desayuno incluido.',
    detail: 'Desde 95 € / noche',
    tag: 'Alojamiento',
    image: '/images/33348420.jpg',
  },
  {
    name: 'Suite Can Segura',
    description: 'Nuestra suite más exclusiva con terraza privada, bañera de hidromasaje y decoración de época. Una experiencia única.',
    detail: 'Desde 175 € / noche',
    tag: 'Suite',
    image: '/images/33348428.jpg',
  },
  {
    name: 'Habitación Superior',
    description: 'Más espacio, más luz y más confort. Con salón independiente, chimenea y vistas panorámicas al entorno natural.',
    detail: 'Desde 130 € / noche',
    tag: 'Alojamiento',
    image: '/images/33348430.jpg',
  },
  {
    name: 'Restaurante & Terraza',
    description: 'Cocina catalana de proximidad con producto de temporada. Terraza exterior con vistas al jardín para cenas al aire libre.',
    detail: 'Abierto cada día',
    tag: 'Gastronomía',
    image: '/images/33348436.jpg',
  },
  {
    name: 'Jardín & Piscina',
    description: 'Piscina exterior rodeada de vegetación mediterránea. Tumbonas, hamacas y el sonido de la naturaleza como música de fondo.',
    detail: 'Incluido en la estancia',
    tag: 'Bienestar',
    image: '/images/33348439.jpg',
  },
  {
    name: 'Eventos & Celebraciones',
    description: 'Bodas, aniversarios y reuniones de empresa en un entorno único. Espacios interiores y exteriores totalmente adaptables.',
    detail: 'Consultar disponibilidad',
    tag: 'Eventos',
    image: '/images/33348449.jpg',
  },
]
</script>

<template>
  <section id="servicios" class="services" ref="sectionRef">
    <div class="container">
      <div class="services-header reveal">
        <span class="section-label">Nuestros Servicios</span>
        <h2 class="section-title">
          Todo lo que necesitas<br /><em>bajo el mismo techo</em>
        </h2>
        <p class="section-subtitle">
          Alojamiento con encanto, gastronomía local y espacios para celebrar los
          momentos que importan. Can Segura, tu casa en Cataluña.
        </p>
        <div class="divider"></div>
      </div>

      <div class="services-grid">
        <article
          v-for="(service, i) in services"
          :key="service.name"
          class="service-card reveal"
          :class="`reveal-delay-${(i % 3) + 1}`"
        >
          <div class="service-img-wrap">
            <img :src="service.image" :alt="service.name" class="service-img" />
            <span class="service-tag">{{ service.tag }}</span>
          </div>
          <div class="service-body">
            <h3 class="service-name">{{ service.name }}</h3>
            <p class="service-desc">{{ service.description }}</p>
            <div class="service-footer">
              <span class="service-detail">{{ service.detail }}</span>
            </div>
          </div>
        </article>
      </div>
    </div>
  </section>
</template>

<style scoped>
.services {
  padding: 8rem 0;
  background: var(--bg-secondary);
  position: relative;
}
.services::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 1px;
  background: linear-gradient(to right, transparent, var(--border-accent), transparent);
}

.services-header {
  text-align: center;
  margin-bottom: 4rem;
}
.services-header em { color: var(--accent); font-style: italic; }
.services-header .section-subtitle { margin: 0 auto; text-align: center; }
.services-header .divider { margin: 1.5rem auto; }

.services-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 1.75rem;
}

.service-card {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: var(--radius-lg);
  overflow: hidden;
  transition: transform var(--transition), box-shadow var(--transition), border-color var(--transition);
}
.service-card:hover {
  transform: translateY(-5px);
  box-shadow: var(--shadow-hover);
  border-color: var(--stone);
}

.service-img-wrap {
  position: relative;
  height: 210px;
  overflow: hidden;
}
.service-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  transition: transform 0.55s ease;
}
.service-card:hover .service-img { transform: scale(1.06); }

.service-tag {
  position: absolute;
  top: 1rem; left: 1rem;
  font-size: 0.65rem;
  font-weight: 700;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  color: #fff;
  background: var(--accent);
  padding: 0.25rem 0.7rem;
  border-radius: 2px;
}

.service-body { padding: 1.5rem; }

.service-name {
  font-family: var(--font-serif);
  font-size: 1.2rem;
  font-weight: 600;
  color: var(--text-primary);
  margin-bottom: 0.6rem;
  line-height: 1.3;
}

.service-desc {
  font-size: 0.875rem;
  color: var(--text-muted);
  line-height: 1.65;
  margin-bottom: 1.25rem;
}

.service-footer {
  border-top: 1px solid var(--border);
  padding-top: 1rem;
  display: flex;
  justify-content: flex-end;
}
.service-detail {
  font-family: var(--font-serif);
  font-size: 1rem;
  font-weight: 600;
  color: var(--accent);
}

@media (max-width: 1024px) { .services-grid { grid-template-columns: repeat(2, 1fr); } }
@media (max-width: 640px) { .services-grid { grid-template-columns: 1fr; } }
</style>
