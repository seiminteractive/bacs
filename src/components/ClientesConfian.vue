<script setup>
import { computed } from 'vue'

const clientes = computed(() => {
  const baseClientes = [
    { id: 1, nombre: 'Logística Premium', logo: '../src/assets/img/new-volvo-logo.png' },
    { id: 2, nombre: 'TransExpress Global', logo: '../src/assets/img/new-volvo-logo.png' },
    { id: 3, nombre: 'Fleet Solutions', logo: '../src/assets/img/new-volvo-logo.png' },
    { id: 4, nombre: 'Cargo Express', logo: '../src/assets/img/new-volvo-logo.png' },
    { id: 5, nombre: 'Delivery Network', logo: '../src/assets/img/new-volvo-logo.png' },
    { id: 6, nombre: 'Maritime Logistics', logo: '../src/assets/img/new-volvo-logo.png' },
  ]
  // Duplicar clientes varias veces para efecto infinito suave
  return [...baseClientes, ...baseClientes, ...baseClientes]
})
</script>

<style scoped>
@keyframes scroll-left {
  0% {
    transform: translateX(0);
  }
  100% {
    transform: translateX(-66.666%);
  }
}

.carousel-wrapper {
  animation: scroll-left 30s linear infinite;
}
</style>

<template>
  <section class="py-20 md:py-24 bg-gray-50 overflow-hidden">
    
    <!-- Header centrado -->
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="text-center mb-12">
        <h2 class="text-3xl md:text-4xl font-bold font-primary text-secondary mb-3">
          Clientes que confían en nosotros
        </h2>
        <p class="text-lg text-secondary font-secondary max-w-2xl mx-auto">
          Empresas líderes en logística y transporte en toda la región confían en Bacs para su protección.
        </p>
      </div>
    </div>

    <!-- Carousel 100vw -->
    <div class="relative w-screen left-1/2 right-1/2 -ml-[50vw] -mr-[50vw] overflow-hidden">
      
      <!-- Fade izquierdo -->
      <div class="pointer-events-none absolute top-0 left-0 h-full w-32 z-10 bg-gradient-to-r from-gray-50 to-transparent"></div>
      
      <!-- Fade derecho -->
      <div class="pointer-events-none absolute top-0 right-0 h-full w-32 z-10 bg-gradient-to-l from-gray-50 to-transparent"></div>

      <!-- Carousel con animación CSS -->
      <div class="carousel-wrapper flex gap-8 px-4 sm:px-6 lg:px-8 py-12">
        <div v-for="cliente in clientes" :key="`${cliente.id}-${Math.random()}`" class="flex-shrink-0 w-full sm:w-1/2 lg:w-1/4 xl:w-1/6">
          <div
            class="
              bg-white rounded-xl p-6 h-32
              flex items-center justify-center
              shadow-sm hover:shadow-md transition-all duration-300
              border border-gray-100 hover:border-primary
              group cursor-pointer
            "
          >
            <img
              :src="cliente.logo"
              :alt="cliente.nombre"
              class="max-w-full max-h-full object-contain opacity-60 group-hover:opacity-100 transition-opacity duration-300"
            />
          </div>
        </div>
      </div>

    </div>

    <!-- Indicador -->
    <div class="text-center mt-8 px-4">
      <p class="text-sm text-secondary font-secondary">
        Confían en nosotros más de 50 empresas en el sector logístico y de transporte
      </p>
    </div>

  </section>
</template>
