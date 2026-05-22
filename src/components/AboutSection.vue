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
    { threshold: 0.15 }
  )
  if (sectionRef.value) observer.observe(sectionRef.value)
})
</script>

<template>
  <section id="nosotros" class="about" ref="sectionRef">
    <div class="container about-grid">
      <div class="about-image-wrap reveal">
        <img
          src="/images/491444150_17844934254461946_5165182295044683036_n.jpg"
          alt="Can Segura Hotel & Restaurant"
          class="about-img"
        />
        <div class="about-img-badge">
          <span class="badge-icon">🏡</span>
          <span class="badge-label">Masia catalana</span>
        </div>
      </div>

      <div class="about-content">
        <span class="section-label reveal">Nuestra Historia</span>
        <h2 class="section-title reveal reveal-delay-1">
          Tradición y confort<br />en <em>Can Segura</em>
        </h2>
        <div class="divider reveal reveal-delay-1"></div>
        <p class="about-text reveal reveal-delay-2">
          Can Segura es una antigua masia catalana transformada con mimo en un hotel
          boutique de carácter íntimo. Rodeada de naturaleza, olivos centenarios y
          el silencio que solo el campo catalán puede ofrecer, es el lugar perfecto
          para desconectar sin renunciar al confort ni al buen comer.
        </p>
        <p class="about-text reveal reveal-delay-3">
          Nuestro restaurante apuesta por la cocina de proximidad: productos de la
          huerta propia, carnes locales y una carta de vinos cuidadosamente
          seleccionada entre las mejores denominaciones catalanas.
        </p>

        <div class="about-features reveal reveal-delay-4">
          <div class="feature">
            <span class="feature-icon">🛏️</span>
            <span class="feature-label">Alojamiento</span>
          </div>
          <div class="feature">
            <span class="feature-icon">🍽️</span>
            <span class="feature-label">Restaurante</span>
          </div>
          <div class="feature">
            <span class="feature-icon">🌿</span>
            <span class="feature-label">Naturaleza</span>
          </div>
          <div class="feature">
            <span class="feature-icon">🎉</span>
            <span class="feature-label">Eventos</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
.about {
  padding: 8rem 0;
  background: var(--bg-primary);
  position: relative;
}

.about-grid {
  display: grid;
  grid-template-columns: 1fr 1.1fr;
  gap: 6rem;
  align-items: center;
}

.about-image-wrap { position: relative; }

.about-img {
  width: 100%;
  height: 560px;
  object-fit: cover;
  border-radius: var(--radius-lg);
  box-shadow: var(--shadow-hover);
}

.about-img-badge {
  position: absolute;
  bottom: -1.25rem;
  right: -1.25rem;
  background: var(--accent);
  color: #fff;
  padding: 1rem 1.4rem;
  border-radius: var(--radius-md);
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.25rem;
  box-shadow: var(--shadow-hover);
}
.badge-icon { font-size: 1.5rem; }
.badge-label {
  font-size: 0.65rem;
  font-weight: 600;
  letter-spacing: 0.12em;
  text-transform: uppercase;
  opacity: 0.9;
}

.about-content em { font-style: italic; color: var(--accent); }

.about-text {
  color: var(--text-muted);
  line-height: 1.8;
  margin-bottom: 1.25rem;
  font-size: 0.97rem;
}

.about-features {
  display: flex;
  gap: 2rem;
  margin-top: 2.5rem;
  padding-top: 2rem;
  border-top: 1px solid var(--border);
  flex-wrap: wrap;
}
.feature {
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 0.4rem;
}
.feature-icon { font-size: 1.5rem; }
.feature-label {
  font-size: 0.7rem;
  font-weight: 600;
  letter-spacing: 0.08em;
  text-transform: uppercase;
  color: var(--text-muted);
}

@media (max-width: 900px) {
  .about-grid { grid-template-columns: 1fr; gap: 3rem; }
  .about-img { height: 360px; }
  .about-img-badge { right: 1rem; }
}
</style>
