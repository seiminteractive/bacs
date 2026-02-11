<script setup>
import Navbar from './components/Navbar.vue'
import Hero from './components/Hero.vue'
import Nosotros from './components/Nosotros.vue'
import Servicios from './components/Servicios.vue'
import ComoTrabajamos from './components/ComoTrabajamos.vue'
import ClientesConfian from './components/ClientesConfian.vue'
import Contacto from './components/Contacto.vue'
import Footer from './components/Footer.vue'
</script>

<template>
  <div class="bg-white">
    <Navbar />
    
    <!-- Secciones principales -->
    <Hero />
    <ClientesConfian />
    <Nosotros />
    <Servicios />
    <ComoTrabajamos />
    <Contacto />

    <!-- Footer -->
    <Footer />
  </div>
</template>
