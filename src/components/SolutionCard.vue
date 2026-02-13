<script setup>
import { computed } from 'vue'

/**
 * SolutionCard - Componente presentacional para mostrar una solución
 * 
 * Responsabilidad única: Renderizar una tarjeta con información de una solución
 * No contiene lógica de negocio
 */

const props = defineProps({
  /**
   * Ícono del Phosphor Icons
   * @type {Object}
   */
  icon: {
    type: Object,
    required: true,
  },
  /**
   * Título de la solución
   * @type {String}
   */
  title: {
    type: String,
    required: true,
  },
  /**
   * Descripción breve
   * @type {String}
   */
  description: {
    type: String,
    required: true,
  },
})

const cardClasses = computed(() => [
  'h-full bg-white rounded-2xl p-8 shadow-sm border border-gray-100',
  'hover:shadow-lg hover:border-primary transition-all duration-300',
  'cursor-pointer group flex flex-col',
])
</script>

<template>
  <div :class="cardClasses">
    <!-- Ícono -->
    <div class="mb-6">
      <component
        :is="icon"
        :size="30"
        weight="regular"
        :color="'#0128ec'"
        class="group-hover:scale-110 transition-transform duration-300"
      />
    </div>

    <!-- Título -->
    <h3 class="text-xl font-bold text-secondary font-primary mb-3">
      {{ title }}
    </h3>

    <!-- Descripción -->
    <p class="text-secondary text-sm font-secondary leading-relaxed">
      {{ description }}
    </p>
  </div>
</template>
