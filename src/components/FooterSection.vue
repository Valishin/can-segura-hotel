<script setup lang="ts">
const scrollTop = () => window.scrollTo({ top: 0, behavior: 'smooth' })
const year = new Date().getFullYear()
const scrollTo = (id: string) => {
  document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' })
}
</script>

<template>
  <footer class="footer">
    <div class="footer-inner container">
      <div class="footer-brand">
        <button class="footer-logo" @click="scrollTop">
          <span class="logo-text">Can Segura</span>
          <span class="logo-sub">Hotel & Restaurant</span>
        </button>
        <p class="footer-tagline">Masia catalana · Tradición · Naturaleza</p>
      </div>

      <div class="footer-links-grid">
        <div class="footer-col">
          <h5>Navegación</h5>
          <ul>
            <li><button @click="scrollTo('nosotros')">Nosotros</button></li>
            <li><button @click="scrollTo('servicios')">Servicios</button></li>
            <li><button @click="scrollTo('galeria')">Galería</button></li>
            <li><button @click="scrollTo('ubicacion')">Ubicación</button></li>
            <li><button @click="scrollTo('contacto')">Contacto</button></li>
          </ul>
        </div>

        <div class="footer-col">
          <h5>Horario</h5>
          <ul>
            <li><span>Recepción: todos los días</span></li>
            <li><span>Check-in: 14:00 – 21:00</span></li>
            <li><span>Check-out: hasta 12:00</span></li>
            <li><span>Restaurante: 13:00 – 22:00</span></li>
          </ul>
        </div>

        <div class="footer-col">
          <h5>Contacto</h5>
          <ul>
            <li><a href="tel:+34000000000">+34 000 000 000</a></li>
            <li><a href="mailto:info@cansegura.com">info@cansegura.com</a></li>
            <li><span>Carretera de Can Segura, s/n</span></li>
            <li><span>Cataluña</span></li>
          </ul>
        </div>
      </div>
    </div>

    <div class="footer-bottom">
      <div class="container footer-bottom-inner">
        <p>© {{ year }} Can Segura Hotel & Restaurant. Todos los derechos reservados.</p>
        <button class="back-top" @click="scrollTop" aria-label="Volver arriba">↑</button>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  background: var(--bg-secondary);
  border-top: 1px solid var(--border);
}

.footer-inner {
  display: grid;
  grid-template-columns: 1fr 2fr;
  gap: 4rem;
  padding-top: 4rem;
  padding-bottom: 4rem;
  border-bottom: 1px solid var(--border);
}

.footer-logo {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  line-height: 1;
  cursor: pointer;
  margin-bottom: 0.75rem;
}
.logo-text {
  font-family: var(--font-serif);
  font-size: 1.5rem;
  font-weight: 700;
  color: var(--text-primary);
}
.logo-sub {
  font-size: 0.6rem;
  font-weight: 600;
  letter-spacing: 0.25em;
  text-transform: uppercase;
  color: var(--accent);
  margin-top: 3px;
}
.footer-tagline {
  font-size: 0.8rem;
  color: var(--text-faint);
  letter-spacing: 0.05em;
}

.footer-links-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 2rem;
}

.footer-col h5 {
  font-size: 0.7rem;
  font-weight: 700;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--accent);
  margin-bottom: 1.25rem;
}

.footer-col ul { list-style: none; display: flex; flex-direction: column; gap: 0.55rem; }

.footer-col li button,
.footer-col li a,
.footer-col li span {
  font-size: 0.875rem;
  color: var(--text-muted);
  transition: color var(--transition);
  display: inline-block;
}
.footer-col li button:hover,
.footer-col li a:hover { color: var(--accent); }

.footer-bottom { padding: 1.25rem 0; }
.footer-bottom-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.footer-bottom p { font-size: 0.78rem; color: var(--text-faint); }

.back-top {
  width: 36px; height: 36px;
  border: 1px solid var(--border);
  border-radius: 50%;
  font-size: 0.9rem;
  color: var(--text-muted);
  display: flex;
  align-items: center;
  justify-content: center;
  transition: border-color var(--transition), color var(--transition);
}
.back-top:hover { border-color: var(--accent); color: var(--accent); }

@media (max-width: 900px) {
  .footer-inner { grid-template-columns: 1fr; gap: 2.5rem; }
  .footer-links-grid { grid-template-columns: 1fr 1fr; }
}
@media (max-width: 500px) {
  .footer-links-grid { grid-template-columns: 1fr; }
}
</style>
