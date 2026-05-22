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
  <section id="ubicacion" class="location" ref="sectionRef">
    <div class="container location-grid">
      <div class="location-info">
        <span class="section-label reveal">Cómo llegar</span>
        <h2 class="section-title reveal reveal-delay-1">
          Fácil de encontrar,<br /><em>difícil de olvidar</em>
        </h2>
        <div class="divider reveal reveal-delay-1"></div>

        <div class="info-cards">
          <div class="info-card reveal reveal-delay-2">
            <div class="info-icon">📍</div>
            <div>
              <h4>Dirección</h4>
              <!-- Actualiza con la dirección real -->
              <p>Carretera de Can Segura, s/n<br />Cataluña</p>
            </div>
          </div>

          <div class="info-card reveal reveal-delay-2">
            <div class="info-icon">🕐</div>
            <div>
              <h4>Recepción</h4>
              <p>Check-in: 14:00 – 21:00<br />Check-out: hasta las 12:00<br />Restaurante: 13:00 – 22:00</p>
            </div>
          </div>

          <div class="info-card reveal reveal-delay-3">
            <div class="info-icon">📞</div>
            <div>
              <h4>Teléfono</h4>
              <!-- Actualiza con el teléfono real -->
              <p><a href="tel:+34000000000">+34 000 000 000</a></p>
            </div>
          </div>

          <div class="info-card reveal reveal-delay-3">
            <div class="info-icon">✉️</div>
            <div>
              <h4>Email</h4>
              <!-- Actualiza con el email real -->
              <p><a href="mailto:info@cansegura.com">info@cansegura.com</a></p>
            </div>
          </div>
        </div>
      </div>

      <div class="location-map reveal reveal-delay-2">
        <!--
          MAPA: reemplaza el src del iframe con el embed de Google Maps real.
          Google Maps → busca → Compartir → Incorporar un mapa → copia el iframe
        -->
        <iframe
          src="https://www.google.com/maps/embed?pb=!1m18!1m12!1m3!1d190000!2d2.1!3d41.7!2m3!1f0!2f0!3f0!3m2!1i1024!2i768!4f13.1!3m3!1m2!1s0x12a4a2000000001%3A0x0!2sCatalu%C3%B1a!5e0!3m2!1ses!2ses!4v1700000000000"
          width="100%"
          height="100%"
          style="border:0;"
          allowfullscreen
          loading="lazy"
          referrerpolicy="no-referrer-when-downgrade"
          title="Ubicación Can Segura Hotel"
        ></iframe>
      </div>
    </div>
  </section>
</template>

<style scoped>
.location {
  padding: 8rem 0;
  background: var(--bg-secondary);
  position: relative;
}
.location::before {
  content: '';
  position: absolute;
  top: 0; left: 0; right: 0;
  height: 1px;
  background: linear-gradient(to right, transparent, var(--border-accent), transparent);
}

.location-grid {
  display: grid;
  grid-template-columns: 1fr 1.2fr;
  gap: 5rem;
  align-items: start;
}

.location-info em { color: var(--accent); font-style: italic; }

.info-cards {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 1rem;
  margin-top: 2rem;
}

.info-card {
  background: var(--bg-card);
  border: 1px solid var(--border);
  border-radius: var(--radius-md);
  padding: 1.4rem;
  display: flex;
  gap: 0.85rem;
  align-items: flex-start;
  transition: border-color var(--transition), box-shadow var(--transition);
}
.info-card:hover {
  border-color: var(--stone);
  box-shadow: var(--shadow-card);
}

.info-icon { font-size: 1.3rem; flex-shrink: 0; margin-top: 0.1rem; }

.info-card h4 {
  font-family: var(--font-serif);
  font-size: 0.95rem;
  font-weight: 600;
  color: var(--text-primary);
  margin-bottom: 0.35rem;
}
.info-card p {
  font-size: 0.86rem;
  color: var(--text-muted);
  line-height: 1.6;
}
.info-card a {
  color: var(--accent);
  transition: color var(--transition);
}
.info-card a:hover { color: var(--accent-dark); }

.location-map {
  border-radius: var(--radius-lg);
  overflow: hidden;
  height: 460px;
  border: 1px solid var(--border);
  box-shadow: var(--shadow-card);
}

@media (max-width: 900px) {
  .location-grid { grid-template-columns: 1fr; gap: 3rem; }
  .location-map { height: 300px; }
  .info-cards { grid-template-columns: 1fr; }
}
</style>
