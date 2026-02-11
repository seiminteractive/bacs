<script setup>
/**
 * Nosotros - Sección sobre la empresa
 * 
 * Responsabilidad: Comunicar la propuesta de valor, experiencia y especialización
 * Solo presentación, sin lógica de negocio
 */
</script>

<template>
  <section id="nosotros" class="py-20 md:py-32 px-4 sm:px-6 lg:px-8 bg-white relative overflow-hidden">
    <!-- Decoración de fondo - Degradados sutiles -->
    <div class="absolute top-20 left-0 w-96 h-96 bg-blue-100 rounded-full blur-3xl opacity-15 -z-10"></div>
    <div class="absolute bottom-0 right-0 w-80 h-80 bg-blue-50 rounded-full blur-3xl opacity-20 -z-10"></div>
    
    <div class="max-w-6xl mx-auto relative z-10">
      <div class="grid grid-cols-1 md:grid-cols-2 gap-12 lg:gap-16 items-center">
        <!-- Contenido -->
        <div>
          <p class="text-sm font-secondary text-primary uppercase tracking-widest mb-4">
            Sobre nosotros
          </p>
          <h2 class="text-4xl md:text-5xl font-bold font-primary text-secondary mb-6 leading-tight">
            Seguros diseñados por expertos
          </h2>
          <p class="text-lg text-secondary font-secondary mb-6 leading-relaxed opacity-80">
            Somos especialistas en seguros para empresas logísticas y de transporte. Con más de 15 años de experiencia, entendemos los desafíos únicos del sector.
          </p>
          <p class="text-lg text-secondary font-secondary mb-8 leading-relaxed opacity-80">
            Nuestra misión es simple: ofrecer protección integral con procesos transparentes, cotizaciones rápidas y un equipo siempre disponible.
          </p>
          
          <!-- Stats -->
          <div class="grid grid-cols-3 gap-8 pt-8 border-t border-gray-100">
            <div>
              <div class="text-3xl font-bold text-primary font-primary">50+</div>
              <p class="text-sm text-secondary font-secondary opacity-70 mt-2">Empresas protegidas</p>
            </div>
            <div>
              <div class="text-3xl font-bold text-primary font-primary">15+</div>
              <p class="text-sm text-secondary font-secondary opacity-70 mt-2">Años de expertise</p>
            </div>
            <div>
              <div class="text-3xl font-bold text-primary font-primary">24/7</div>
              <p class="text-sm text-secondary font-secondary opacity-70 mt-2">Soporte disponible</p>
            </div>
          </div>
        </div>

        <!-- Imagen visual -->
        <div class="relative">
          <!-- Degradado de fondo detrás -->
          <div class="absolute inset-0 bg-gradient-to-br from-blue-100 via-blue-50 to-transparent rounded-3xl blur-2xl opacity-40 -z-10"></div>
          
          <div class="bg-gradient-to-br from-blue-100 to-blue-50 rounded-3xl h-96 flex items-center justify-center relative border border-blue-100 shadow-xl overflow-hidden">
            <img 
              src="https://www.icontainers.com/static/ad4954fa171f0b811c89485d493d9383/801a4/Ocean_dc21ab4cae_a4334f978d.jpg" 
              alt="Logística" 
              class="w-full h-full object-cover rounded-2xl"
            />
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
