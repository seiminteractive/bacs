<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import { PhList, PhX } from '@phosphor-icons/vue'

const menuOpen = ref(false)
const isScrolled = ref(false)

const toggleMenu = () => {
  menuOpen.value = !menuOpen.value
}

const navLinks = [
  { label: 'Inicio', href: '#home' },
  { label: 'Nosotros', href: '#nosotros' },
  { label: 'Servicios', href: '#servicios' },
  { label: 'Cómo Trabajamos', href: '#como-trabajamos' },
  { label: 'Contacto', href: '#contacto' },
]

const handleNavClick = () => {
  menuOpen.value = false
}

/**
 * Detectar scroll para cambiar el estilo del navbar
 */
const handleScroll = () => {
  isScrolled.value = window.scrollY > 10
}

onMounted(() => {
  window.addEventListener('scroll', handleScroll)
})

onUnmounted(() => {
  window.removeEventListener('scroll', handleScroll)
})
</script>

<template>
  <header
    :class="[
      'fixed w-full top-0 z-50 transition-all duration-300',
      isScrolled
        ? 'bg-white/20 backdrop-blur-md border-b border-gray-200/50 shadow-md'
        : 'bg-transparent border-0 border-gray-100'
    ]"
  >
    <nav class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="flex justify-between items-center h-16 md:h-20">
        <!-- Logo -->
        <a href="#home" class="flex items-center gap-2 group" @click="handleNavClick">
          <img 
            src="/BacsLogoAzul.png" 
            alt="Bacs Logo" 
            class="h-10 w-auto group-hover:scale-110 transition-transform"
          />
        </a>

        <!-- Desktop Navigation -->
        <div class="hidden md:flex items-center gap-8">
          <a
            v-for="link in navLinks"
            :key="link.href"
            :href="link.href"
            class="text-secondary text-sm font-secondary hover:text-primary transition-colors duration-200"
          >
            {{ link.label }}
          </a>
        </div>

        <!-- CTA Buttons -->
        <div class="hidden md:flex items-center gap-4">
          <a
            href="#contacto"
            class="bg-primary text-white px-6 py-2.5 rounded-lg font-primary font-bold text-sm hover:shadow-lg transition-all duration-200 hover:scale-105"
          >
            Cotizar
          </a>
        </div>

        <!-- Mobile Menu Button -->
        <button
          @click="toggleMenu"
          class="md:hidden p-2 rounded-lg hover:bg-gray-100 transition-colors"
        >
          <PhList v-if="!menuOpen" :size="24" weight="bold" class="text-secondary" />
          <PhX v-else :size="24" weight="bold" class="text-secondary" />
        </button>
      </div>

      <!-- Mobile Navigation -->
      <div
        v-if="menuOpen"
        class="md:hidden pb-4 border-t border-gray-100"
      >
        <div class="pt-4 space-y-3">
          <a
            v-for="link in navLinks"
            :key="link.href"
            :href="link.href"
            class="block text-secondary hover:text-primary transition-colors py-2 text-sm font-secondary"
            @click="handleNavClick"
          >
            {{ link.label }}
          </a>
          <div class="flex gap-3 pt-4 border-t border-gray-100">
            <a
              href="#contacto"
              class="flex-1 text-secondary text-sm font-secondary border border-secondary rounded-lg py-2 hover:bg-gray-50 transition-colors text-center"
              @click="handleNavClick"
            >
              Contacto
            </a>
            <a
              href="#contacto"
              class="flex-1 bg-primary text-white px-4 py-2 rounded-lg font-primary font-bold text-sm hover:shadow-lg transition-all text-center"
              @click="handleNavClick"
            >
              Cotizar
            </a>
          </div>
        </div>
      </div>
    </nav>
  </header>
</template>
