<script setup>
import { computed } from 'vue'
import { PhEnvelope, PhPhone, PhLinkedinLogo, PhInstagramLogo } from '@phosphor-icons/vue'

/**
 * Footer - Sección de pie de página
 * 
 * Responsabilidad: Mostrar información de contacto, links útiles y créditos
 * Datos separados de presentación
 */

const currentYear = computed(() => new Date().getFullYear())

const quickLinks = [
  { label: 'Inicio', href: '#home' },
  { label: 'Servicios', href: '#servicios' },
  { label: 'Nosotros', href: '#nosotros' },
  { label: 'Contacto', href: '#contacto' },
]

const contactInfo = [
  { icon: PhPhone, label: 'Teléfono', value: '+1 (555) 123-4567' },
  { icon: PhEnvelope, label: 'Email', value: 'info@bacs.com' },
]

const socialLinks = [
  { icon: PhLinkedinLogo, label: 'LinkedIn', href: '#' },
  { icon: PhInstagramLogo, label: 'Instagram', href: '#' },
]
</script>

<template>
  <footer class="bg-secondary text-white">
    <!-- Main Footer Content -->
    <div class="py-16 md:py-20 px-4 sm:px-6 lg:px-8 border-b border-white border-opacity-10">
      <div class="max-w-7xl mx-auto">
        <div class="grid grid-cols-1 md:grid-cols-4 gap-12">
          <!-- Logo y descripción -->
          <div class="md:col-span-1">
            <img 
              src="/BacsLogoBlanco.png" 
              alt="Bacs Logo" 
              class="h-12 w-auto mb-4 opacity-90 hover:opacity-100 transition-opacity"
            />
            <p class="text-sm font-secondary opacity-70 leading-relaxed">
              Seguros especializados para empresas de logística y transporte.
            </p>
          </div>

          <!-- Links rápidos -->
          <div>
            <h3 class="font-primary font-bold text-lg mb-6">Enlaces</h3>
            <ul class="space-y-3">
              <li v-for="link in quickLinks" :key="link.href">
                <a
                  :href="link.href"
                  class="text-sm font-secondary opacity-70 hover:opacity-100 hover:text-primary transition-all duration-200"
                >
                  {{ link.label }}
                </a>
              </li>
            </ul>
          </div>

          <!-- Información de contacto -->
          <div>
            <h3 class="font-primary font-bold text-lg mb-6">Contacto</h3>
            <ul class="space-y-4">
              <li v-for="info in contactInfo" :key="info.label" class="flex items-start gap-3">
                <component
                  :is="info.icon"
                  :size="20"
                  weight="bold"
                  class="flex-shrink-0 mt-0.5"
                />
                <div>
                  <p class="text-xs font-secondary opacity-60 mb-1">{{ info.label }}</p>
                  <p class="text-sm font-secondary opacity-90">{{ info.value }}</p>
                </div>
              </li>
            </ul>
          </div>

          <!-- Redes sociales -->
          <div>
            <h3 class="font-primary font-bold text-lg mb-6">Síguenos</h3>
            <div class="flex gap-4">
              <a
                v-for="social in socialLinks"
                :key="social.label"
                :href="social.href"
                :title="social.label"
                class="w-10 h-10 rounded-lg bg-white bg-opacity-10 flex items-center justify-center hover:bg-opacity-20 transition-all duration-200 group"
              >
                <component
                  :is="social.icon"
                  :size="20"
                  weight="bold"
                  class="group-hover:text-primary transition-colors"
                />
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>

    <!-- Bottom Footer -->
    <div class="py-8 px-4 sm:px-6 lg:px-8">
      <div class="max-w-7xl mx-auto">
        <div class="flex flex-col md:flex-row justify-between items-center gap-6">
          <!-- Copyright -->
          <p class="font-secondary text-sm opacity-70 text-center md:text-left">
            © {{ currentYear }} Bacs. Todos los derechos reservados.
          </p>

          <!-- Créditos de desarrollo -->
          <div class="text-center">
            <p class="text-xs font-secondary opacity-60 mb-3">
              Desarrollado por
            </p>
            <a
              href="#"
              target="_blank"
              rel="noopener noreferrer"
              class="inline-block hover:scale-110 transition-transform"
              title="Visit developer website"
            >
              <img 
                src="/vite.svg" 
                alt="Developer Logo" 
                class="h-8 w-auto opacity-60 hover:opacity-100 transition-opacity"
              />
            </a>
          </div>

          <!-- Legal links -->
          <div class="flex gap-6 text-xs font-secondary opacity-70">
            <a href="#" class="hover:opacity-100 transition-opacity">Privacidad</a>
            <a href="#" class="hover:opacity-100 transition-opacity">Términos</a>
            <a href="#" class="hover:opacity-100 transition-opacity">Cookies</a>
          </div>
        </div>
      </div>
    </div>
  </footer>
</template>
