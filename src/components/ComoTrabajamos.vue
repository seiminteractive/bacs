<script setup>
import { computed } from 'vue'
import {
  PhMagnifyingGlass,
  PhCheckCircle,
  PhCreditCard,
  PhThumbsUp,
} from '@phosphor-icons/vue'

/**
 * ComoTrabajamos - Sección del proceso
 * 
 * Responsabilidad: Mostrar el flujo de trabajo paso a paso
 * Datos separados de presentación
 */

const pasos = computed(() => [
  {
    numero: '01',
    icon: PhMagnifyingGlass,
    titulo: 'Evaluamos',
    descripcion: 'Analizamos tu operación logística y necesidades específicas.',
  },
  {
    numero: '02',
    icon: PhCheckCircle,
    titulo: 'Diseñamos',
    descripcion: 'Creamos una cobertura personalizada para tu empresa.',
  },
  {
    numero: '03',
    icon: PhCreditCard,
    titulo: 'Cotizamos',
    descripcion: 'Te presentamos opciones transparentes y competitivas.',
  },
  {
    numero: '04',
    icon: PhThumbsUp,
    titulo: 'Protegemos',
    descripcion: 'Tu empresa está cubierta. Soporte 24/7 siempre disponible.',
  },
])
</script>

<template>
  <section id="como-trabajamos" class="py-20 md:py-32 px-4 sm:px-6 lg:px-8 bg-white relative overflow-hidden">
    <!-- Decoración de fondo - Degradados sutiles -->
    <div class="absolute top-0 left-1/3 w-96 h-96 bg-blue-100 rounded-full blur-3xl opacity-15 -z-10"></div>
    <div class="absolute bottom-0 right-0 w-96 h-96 bg-blue-50 rounded-full blur-3xl opacity-20 -z-10"></div>
    
    <div class="max-w-6xl mx-auto relative z-10">
      <!-- Header -->
      <div class="text-center mb-16">
        <p class="text-sm font-secondary text-primary uppercase tracking-widest mb-4">
          Proceso Simple
        </p>
        <h2 class="text-4xl md:text-5xl font-bold font-primary text-secondary mb-4">
          Cómo Trabajamos
        </h2>
        <p class="text-xl text-secondary font-secondary max-w-2xl mx-auto opacity-80">
          Un proceso claro y directo, diseñado para tu comodidad.
        </p>
      </div>

      <!-- Grid de pasos -->
      <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8 lg:auto-rows-fr">
        <div
          v-for="(paso, index) in pasos"
          :key="paso.numero"
          class="relative"
        >
          <!-- Línea conectora (solo en desktop) -->
          <div
            v-if="index < pasos.length - 1"
            class="hidden lg:block absolute top-20 -right-4 w-8 h-0.5 bg-gradient-to-r from-primary to-transparent"
          ></div>

          <!-- Card del paso -->
          <div class="bg-white rounded-2xl p-8 border border-gray-100 hover:border-primary hover:shadow-lg transition-all duration-300 relative group h-full flex flex-col">
            <!-- Degradado de fondo en hover -->
            <div class="absolute inset-0 bg-gradient-to-br from-blue-50 to-transparent opacity-0 group-hover:opacity-100 transition-opacity duration-300 rounded-2xl -z-10"></div>
            
            <!-- Número -->
            <div class="text-5xl font-bold text-primary font-primary opacity-20 mb-4 group-hover:opacity-30 transition-opacity">
              {{ paso.numero }}
            </div>

            <!-- Ícono -->
            <div class="mb-6">
              <component
                :is="paso.icon"
                :size="40"
                weight="regular"
                :color="'#0128ec'"
                class="group-hover:scale-110 transition-transform duration-300"
              />
            </div>

            <!-- Título -->
            <h3 class="text-xl font-bold text-secondary font-primary mb-3">
              {{ paso.titulo }}
            </h3>

            <!-- Descripción -->
            <p class="text-secondary text-sm font-secondary opacity-70 leading-relaxed flex-grow">
              {{ paso.descripcion }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
