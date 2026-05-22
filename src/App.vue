<script setup lang="ts">
import NavBar from './components/NavBar.vue'
import HeroSection from './components/HeroSection.vue'
import AboutSection from './components/AboutSection.vue'
import MenuSection from './components/MenuSection.vue'
import GallerySection from './components/GallerySection.vue'
import LocationSection from './components/LocationSection.vue'
import ContactSection from './components/ContactSection.vue'
import FooterSection from './components/FooterSection.vue'
</script>

<template>
  <NavBar />
  <main>
    <HeroSection />
    <AboutSection />
    <MenuSection />
    <GallerySection />
    <LocationSection />
    <ContactSection />
  </main>
  <FooterSection />
</template>

<style>
@import './assets/main.css';
</style>
