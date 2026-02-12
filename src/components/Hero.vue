<script setup>
/**
 * Hero - Sección principal de la landing
 * 
 * Responsabilidad: Mostrar propuesta de valor clara y transmitir confianza
 * Solo renderiza UI, sin lógica de negocio
 */
</script>

<style scoped>
.hero-bg {
  position: relative;
  background: #f7f9ff;
  overflow: hidden;
}

.hero-bg::before {
  content: '';
  position: absolute;
  inset: 0;
  pointer-events: none;

  background:
    /* IZQUIERDA - Azul más profundo */
    radial-gradient(
      ellipse 50% 60% at -15% 40%,
      rgba(1, 40, 236, 0.55) 0%,
      rgba(1, 40, 236, 0.35) 30%,
      rgba(1, 40, 236, 0.18) 55%,
      transparent 75%
    ),


    /* DERECHA - Azul mucho más claro */
    radial-gradient(
      ellipse 60% 80% at 110% 40%,
      rgba(1, 40, 236, 0.18) 0%,
      rgba(1, 40, 236, 0.10) 35%,
      transparent 70%
    );

  filter: blur(110px);
}

.hero-bg::after {
  content: '';
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  height: 100px; /* ajustable */

  background: linear-gradient(
    to bottom,
    rgba(247, 249, 255, 0) 0%,
    rgba(247, 249, 255, 0.6) 40%,
    #f9fafb 100%
  );

  pointer-events: none;
}


</style>

<template>
  <section id="home" class="hero-bg h-screen flex items-center justify-center px-4 sm:px-6 lg:px-8 relative overflow-hidden">
    <!-- Decoración de fondo adicional -->
    <div class="absolute top-10 right-10 w-96 h-96 bg-white rounded-full blur-3xl opacity-10 -z-10"></div>
    
    <div class="max-w-5xl mx-auto text-center relative z-10">
      <!-- Badge -->
      <div class="inline-flex items-center gap-0 bg-white/20 border border-blue-100 rounded-full px-6 py-2 mb-8">
        <div class="w-2 h-2 bg-primary rounded-full"></div>
        <span class="backdrop-blur-md bg-white/20 border border-white/40 text-secondary px-3 py-1 rounded-lg font-primary font-semibold text-sm hover:bg-white/30 hover:border-white/60 transition-all duration-300">Broker en seguros logísticos</span>
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
        <button class="bg-primary text-white px-6 py-2 rounded-full font-primary font-semibold text-sm hover:shadow-lg hover:scale-105 transition-all duration-300">
          Cotizar ahora
        </button>
        <button class="backdrop-blur-md bg-white/20 border border-blue-100 text-secondary px-6 py-2 rounded-full font-primary font-semibold text-sm hover:bg-white/30 transition-all duration-300">
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
