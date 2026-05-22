<script setup lang="ts">
const scrollTop = () => window.scrollTo({ top: 0, behavior: 'smooth' })
const year = new Date().getFullYear()
const scrollTo = (id: string) => {
  document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' })
}
</script>

<template>
  <footer class="footer">

    <!-- Franja de reservas -->
    <div class="reservas-bar">
      <div class="container reservas-inner">
        <div class="reservas-text">
          <span class="reservas-label">¿Listo para tu escapada?</span>
          <p>Consulta disponibilidad y reserva tu estancia en Can Segura</p>
        </div>
        <button class="reservas-btn">Reservar ahora</button>
      </div>
    </div>

    <div class="footer-inner container">
      <!-- Brand + redes -->
      <div class="footer-brand">
        <button class="footer-logo" @click="scrollTop">
          <span class="logo-text">Can Segura</span>
          <span class="logo-sub">Hotel & Restaurant</span>
        </button>
        <p class="footer-tagline">Masia catalana · Tradición · Naturaleza</p>

        <div class="social-links">
          <!-- Instagram -->
          <a href="#" class="social-icon" aria-label="Instagram">
            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round">
              <rect x="2" y="2" width="20" height="20" rx="5" ry="5"/>
              <circle cx="12" cy="12" r="4"/>
              <circle cx="17.5" cy="6.5" r="1" fill="currentColor" stroke="none"/>
            </svg>
          </a>
          <!-- Facebook -->
          <a href="#" class="social-icon" aria-label="Facebook">
            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round">
              <path d="M18 2h-3a5 5 0 0 0-5 5v3H7v4h3v8h4v-8h3l1-4h-4V7a1 1 0 0 1 1-1h3z"/>
            </svg>
          </a>
          <!-- TripAdvisor -->
          <a href="#" class="social-icon" aria-label="TripAdvisor">
            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round">
              <circle cx="7" cy="14" r="3"/>
              <circle cx="17" cy="14" r="3"/>
              <path d="M2 9h20M7 9a5 5 0 0 1 10 0"/>
            </svg>
          </a>
          <!-- Google -->
          <a href="#" class="social-icon" aria-label="Google">
            <svg width="18" height="18" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="1.6" stroke-linecap="round" stroke-linejoin="round">
              <circle cx="12" cy="12" r="10"/>
              <path d="M17.5 12H12v2.5h3.2A3.5 3.5 0 0 1 8.5 12a3.5 3.5 0 0 1 6.1-2.3L16.2 8A6 6 0 1 0 18 12"/>
            </svg>
          </a>
        </div>
      </div>

      <!-- Columnas -->
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
        <div class="footer-bottom-right">
          <a href="https://icorebyte.com" target="_blank" rel="noopener" class="made-by">Hecho por icorebyte.com</a>
          <button class="back-top" @click="scrollTop" aria-label="Volver arriba">↑</button>
        </div>
      </div>
    </div>
  </footer>
</template>

<style scoped>
.footer {
  background: var(--bg-secondary);
  border-top: 1px solid var(--border);
}

/* ---- Reservas bar ---- */
.reservas-bar {
  background: var(--accent);
  padding: 2rem 0;
}

.reservas-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 2rem;
  flex-wrap: wrap;
}

.reservas-label {
  display: block;
  font-family: var(--font-serif);
  font-size: 1.3rem;
  font-weight: 600;
  color: #fff;
  margin-bottom: 0.2rem;
}

.reservas-text p {
  font-size: 0.875rem;
  color: rgba(255, 255, 255, 0.75);
}

.reservas-btn {
  font-family: var(--font-sans);
  font-size: 0.85rem;
  font-weight: 700;
  letter-spacing: 0.1em;
  text-transform: uppercase;
  color: var(--accent-dark);
  background: #fff;
  padding: 0.9rem 2.2rem;
  border-radius: var(--radius-sm);
  white-space: nowrap;
  transition: background var(--transition), transform 0.2s;
  box-shadow: 0 4px 16px rgba(0, 0, 0, 0.12);
}
.reservas-btn:hover {
  background: var(--bg-primary);
  transform: translateY(-2px);
}

/* ---- Footer inner ---- */
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
  margin-bottom: 1.5rem;
}

/* ---- Social icons ---- */
.social-links {
  display: flex;
  gap: 0.6rem;
}

.social-icon {
  width: 36px;
  height: 36px;
  border: 1px solid var(--border);
  border-radius: var(--radius-sm);
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--text-muted);
  transition: color var(--transition), border-color var(--transition), background var(--transition);
}
.social-icon:hover {
  color: var(--accent);
  border-color: var(--accent);
  background: rgba(139, 115, 85, 0.06);
}

/* ---- Columns ---- */
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

/* ---- Bottom bar ---- */
.footer-bottom { padding: 1.25rem 0; }
.footer-bottom-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
.footer-bottom p { font-size: 0.78rem; color: var(--text-faint); }

.footer-bottom-right {
  display: flex;
  align-items: center;
  gap: 1.25rem;
}

.made-by {
  font-size: 0.75rem;
  color: var(--text-faint);
  transition: color var(--transition);
}
.made-by:hover { color: var(--accent); }

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
  .reservas-inner { flex-direction: column; align-items: flex-start; }
}
@media (max-width: 500px) {
  .footer-links-grid { grid-template-columns: 1fr; }
}
</style>
