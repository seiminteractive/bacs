<script setup>
import { computed } from 'vue'
import {
  PhShield,
  PhClock,
  PhHeadset,
  PhCheckCircle,
} from '@phosphor-icons/vue'
import SolutionCard from './SolutionCard.vue'

/**
 * NuestraSolucion - Sección que presenta las soluciones de Bacs
 * 
 * Responsabilidad: Orquestar la visualización de tarjetas de soluciones
 * Mantiene separación de datos (soluciones) de la presentación (SolutionCard)
 */

const soluciones = computed(() => [
  {
    id: 'cobertura',
    icon: PhShield,
    title: 'Cobertura Completa',
    description: 'Protección integral para tu flota. Desde responsabilidad civil hasta daños a carga, cubrimos todas tus necesidades.',
  },
  {
    id: 'agilidad',
    icon: PhClock,
    title: 'Cotización Rápida',
    description: 'Obtén cotizaciones en minutos, no en días. Nuestro proceso es transparente y sin complicaciones.',
  },
  {
    id: 'soporte',
    icon: PhHeadset,
    title: 'Soporte 24/7',
    description: 'Equipo especializado siempre disponible. Te acompañamos en cada paso del camino.',
  },
  {
    id: 'transparencia',
    icon: PhCheckCircle,
    title: 'Transparencia Total',
    description: 'Sin sorpresas. Sabes exactamente qué estás cubriendo y qué costo tiene.',
  },
])
</script>

<template>
  <section class="py-20 md:py-32 px-4 sm:px-6 lg:px-8 bg-white">
    <div class="max-w-7xl mx-auto">
      <!-- Header -->
      <div class="text-center mb-16">
        <p class="text-sm font-secondary text-primary uppercase tracking-wider mb-3">
          Nuestra Solución
        </p>
        <h2 class="text-4xl md:text-5xl font-bold font-primary text-secondary mb-4">
          Seguros Diseñados para Logística
        </h2>
        <p class="text-lg text-secondary font-secondary max-w-2xl mx-auto">
          Soluciones especializadas que entienden los retos únicos del transporte y la logística.
        </p>
      </div>

      <!-- Grid de soluciones -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6">
        <SolutionCard
          v-for="solucion in soluciones"
          :key="solucion.id"
          :icon="solucion.icon"
          :title="solucion.title"
          :description="solucion.description"
        />
      </div>
    </div>
  </section>
</template>
