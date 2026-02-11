<script setup>
import { computed } from 'vue'
import {
  PhTruck,
  PhPackage,
  PhShieldCheckered,
  PhCurrencyDollar,
} from '@phosphor-icons/vue'
import SolutionCard from './SolutionCard.vue'

/**
 * Servicios - Sección de servicios/productos
 * 
 * Responsabilidad: Orquestar visualización de servicios
 * Mantiene datos separados de presentación
 */

const servicios = computed(() => [
  {
    id: 'responsabilidad-civil',
    icon: PhShieldCheckered,
    title: 'Responsabilidad Civil',
    description: 'Cobertura integral ante daños causados a terceros durante el transporte.',
  },
  {
    id: 'cobertura-carga',
    icon: PhPackage,
    title: 'Cobertura de Carga',
    description: 'Protección total para tu mercancía en tránsito, sin importar el destino.',
  },
  {
    id: 'vehiculos',
    icon: PhTruck,
    title: 'Seguro de Vehículos',
    description: 'Cobertura completa para tu flota, incluyendo accidentes y robo.',
  },
  {
    id: 'responsabilidad-conductores',
    icon: PhCurrencyDollar,
    title: 'Paquetes Customizados',
    description: 'Diseñamos coberturas a medida según las necesidades de tu empresa.',
  },
])
</script>

<template>
  <section id="servicios" class="py-20 md:py-32 px-4 sm:px-6 lg:px-8 bg-gray-50 relative overflow-hidden">
    <!-- Decoración de fondo - Degradados sutiles -->
    <div class="absolute top-0 right-1/4 w-96 h-96 bg-blue-100 rounded-full blur-3xl opacity-15 -z-10"></div>
    <div class="absolute bottom-20 left-0 w-80 h-80 bg-blue-50 rounded-full blur-3xl opacity-20 -z-10"></div>
    
    <div class="max-w-7xl mx-auto relative z-10">
      <!-- Header -->
      <div class="text-center mb-16">
        <p class="text-sm font-secondary text-primary uppercase tracking-widest mb-4">
          Nuestros Servicios
        </p>
        <h2 class="text-4xl md:text-5xl font-bold font-primary text-secondary mb-4">
          Cobertura Completa
        </h2>
        <p class="text-xl text-secondary font-secondary max-w-2xl mx-auto opacity-80">
          Soluciones especializadas diseñadas para proteger tu negocio logístico.
        </p>
      </div>

      <!-- Grid de servicios -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
        <SolutionCard
          v-for="servicio in servicios"
          :key="servicio.id"
          :icon="servicio.icon"
          :title="servicio.title"
          :description="servicio.description"
        />
      </div>
    </div>
  </section>
</template>
