<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'

const isScrolled = ref(false)
const isMenuOpen = ref(false)

const handleScroll = () => { isScrolled.value = window.scrollY > 60 }

onMounted(() => window.addEventListener('scroll', handleScroll))
onUnmounted(() => window.removeEventListener('scroll', handleScroll))

const scrollTo = (id: string) => {
  isMenuOpen.value = false
  document.getElementById(id)?.scrollIntoView({ behavior: 'smooth' })
}
</script>

<template>
  <nav :class="['navbar', { scrolled: isScrolled, 'menu-open': isMenuOpen }]">
    <div class="nav-inner container">
      <button class="nav-logo" @click="scrollTo('hero')">
        <span class="logo-text">Can Segura</span>
        <span class="logo-sub">Hotel & Restaurant</span>
      </button>

      <ul class="nav-links">
        <li><button @click="scrollTo('nosotros')">Nosotros</button></li>
        <li><button @click="scrollTo('servicios')">Servicios</button></li>
        <li><button @click="scrollTo('galeria')">Galería</button></li>
        <li><button @click="scrollTo('ubicacion')">Ubicación</button></li>
        <li><button class="nav-cta" @click="scrollTo('contacto')">Contacto</button></li>
      </ul>

      <button class="hamburger" :class="{ open: isMenuOpen }" @click="isMenuOpen = !isMenuOpen" aria-label="Menú">
        <span /><span /><span />
      </button>
    </div>

    <div class="mobile-menu" :class="{ open: isMenuOpen }">
      <ul>
        <li><button @click="scrollTo('nosotros')">Nosotros</button></li>
        <li><button @click="scrollTo('servicios')">Servicios</button></li>
        <li><button @click="scrollTo('galeria')">Galería</button></li>
        <li><button @click="scrollTo('ubicacion')">Ubicación</button></li>
        <li><button @click="scrollTo('contacto')">Contacto</button></li>
      </ul>
    </div>
  </nav>
</template>

<style scoped>
.navbar {
  position: fixed;
  top: 0; left: 0; right: 0;
  z-index: 1000;
  transition: background 0.4s ease, box-shadow 0.4s ease;
  background: transparent;
}

.navbar.scrolled {
  background: rgba(250, 248, 244, 0.97);
  backdrop-filter: blur(12px);
  box-shadow: 0 1px 0 var(--border);
}

.nav-inner {
  display: flex;
  align-items: center;
  justify-content: space-between;
  height: 72px;
}

.nav-logo {
  display: flex;
  flex-direction: column;
  align-items: flex-start;
  line-height: 1;
  cursor: pointer;
}

.logo-text {
  font-family: var(--font-serif);
  font-size: 1.35rem;
  font-weight: 700;
  color: #fff;
  letter-spacing: 0.02em;
  transition: color var(--transition);
}

.logo-sub {
  font-size: 0.6rem;
  font-weight: 500;
  letter-spacing: 0.25em;
  text-transform: uppercase;
  color: rgba(255,255,255,0.7);
  margin-top: 2px;
  transition: color var(--transition);
}

.scrolled .logo-text { color: var(--text-primary); }
.scrolled .logo-sub  { color: var(--accent); }

.nav-links {
  display: flex;
  align-items: center;
  gap: 0.25rem;
  list-style: none;
}

.nav-links button {
  font-size: 0.85rem;
  font-weight: 500;
  letter-spacing: 0.05em;
  color: rgba(255,255,255,0.85);
  padding: 0.5rem 0.9rem;
  border-radius: var(--radius-sm);
  transition: color var(--transition);
}

.nav-links button:hover { color: #fff; }

.scrolled .nav-links button { color: var(--text-muted); }
.scrolled .nav-links button:hover { color: var(--text-primary); }

.nav-cta {
  border: 1px solid rgba(255,255,255,0.6) !important;
  color: #fff !important;
  padding: 0.45rem 1.1rem !important;
  border-radius: var(--radius-sm) !important;
  transition: background var(--transition), color var(--transition), border-color var(--transition) !important;
}
.nav-cta:hover {
  background: #fff !important;
  color: var(--accent) !important;
}
.scrolled .nav-cta {
  border-color: var(--accent) !important;
  color: var(--accent) !important;
}
.scrolled .nav-cta:hover {
  background: var(--accent) !important;
  color: #fff !important;
}

.hamburger {
  display: none;
  flex-direction: column;
  gap: 5px;
  padding: 4px;
}
.hamburger span {
  display: block;
  width: 24px; height: 2px;
  background: #fff;
  border-radius: 2px;
  transition: transform 0.3s ease, opacity 0.3s ease;
}
.scrolled .hamburger span { background: var(--text-primary); }
.hamburger.open span:nth-child(1) { transform: translateY(7px) rotate(45deg); }
.hamburger.open span:nth-child(2) { opacity: 0; }
.hamburger.open span:nth-child(3) { transform: translateY(-7px) rotate(-45deg); }

.mobile-menu {
  display: none;
  background: rgba(250, 248, 244, 0.99);
  border-top: 1px solid var(--border);
  overflow: hidden;
  max-height: 0;
  transition: max-height 0.4s ease;
}
.mobile-menu.open { max-height: 400px; }
.mobile-menu ul {
  list-style: none;
  padding: 1.5rem 2rem;
  display: flex;
  flex-direction: column;
  gap: 0.25rem;
}
.mobile-menu button {
  font-size: 1rem;
  color: var(--text-muted);
  padding: 0.75rem 0;
  width: 100%;
  text-align: left;
  border-bottom: 1px solid var(--border);
  transition: color var(--transition);
}
.mobile-menu button:hover { color: var(--accent); }

@media (max-width: 768px) {
  .nav-links { display: none; }
  .hamburger { display: flex; }
  .mobile-menu { display: block; }
}
</style>
