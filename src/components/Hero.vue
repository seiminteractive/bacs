<script setup>
/**
 * Hero - Sección principal de la landing
 * 
 * Responsabilidad: Mostrar propuesta de valor clara y transmitir confianza
 * Solo renderiza UI, sin lógica de negocio
 */
</script>

<template>
  <section id="home" class="h-screen flex items-center justify-center px-4 sm:px-6 lg:px-8 bg-gradient-to-b from-blue-200 via-white to-white relative overflow-hidden">
    <!-- Decoración de fondo -->
    <div class="absolute top-0 right-0 w-96 h-96 bg-blue-100 rounded-full blur-3xl opacity-20 -z-10"></div>
    
    <div class="max-w-5xl mx-auto text-center">
      <!-- Badge -->
      <div class="inline-flex items-center gap-2 bg-white border border-blue-100 rounded-full px-4 py-2 mb-8">
        <div class="w-2 h-2 bg-primary rounded-full"></div>
        <span class="text-sm font-secondary text-secondary">Especialistas en seguros logísticos</span>
      </div>

      <!-- Headline -->
      <h1 class="text-5xl md:text-7xl font-bold font-primary text-secondary mb-6">
        Seguros para
        <span class="relative inline-block">
          <span class="text-primary">tu logística</span>
          <div class="absolute bottom-2 left-0 right-0 h-1 opacity-20"></div>
        </span>
      </h1>

      <!-- Subheadline -->
      <p class="text-xl md:text-2xl text-secondary font-secondary mb-10 max-w-3xl mx-auto leading-relaxed opacity-80">
        Protección integral para empresas de transporte. Cotizaciones rápidas, sin complicaciones, desde tu escritorio.
      </p>

      <!-- CTA Buttons -->
      <div class="flex flex-col sm:flex-row gap-4 justify-center mb-16">
        <button class="bg-primary text-white px-8 py-4 rounded-xl font-primary font-bold text-lg hover:shadow-2xl hover:scale-105 transition-all duration-300">
          Cotizar ahora
        </button>
        <button class="border-2 border-primary text-primary px-8 py-4 rounded-xl font-primary font-bold text-lg hover:bg-blue-50 transition-all duration-300">
          Conocer más
        </button>
      </div>

      <!-- Trust indicator -->
      <div class="text-sm text-secondary font-secondary opacity-70">
        <p>✓ Confían más de 50 empresas logísticas</p>
      </div>
    </div>
  </section>
</template>
