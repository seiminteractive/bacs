<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue'
import gsap from 'gsap'
import LiquidEther from './LiquidEther/LiquidEther.vue'

const sectionRef = ref(null)
const badgeRef = ref(null)
const titleRef = ref(null)
const subtitleRef = ref(null)
const buttonsRef = ref(null)
const trustRef = ref(null)

// Detectar si es mobile
const isMobile = () => window.innerWidth < 768

onMounted(() => {
  // Crear timeline para animaciones del Hero
  const tl = gsap.timeline()

  // Animación del badge - fade in con movimiento sutil hacia arriba
  tl.fromTo(
    badgeRef.value,
    {
      opacity: 0,
      y: isMobile() ? 15 : 20,
    },
    {
      opacity: 1,
      y: 0,
      duration: 0.8,
      ease: 'power2.out',
    },
    0
  )

  // Animación del título - fade in con movimiento hacia arriba
  tl.fromTo(
    titleRef.value,
    {
      opacity: 0,
      y: isMobile() ? 25 : 35,
    },
    {
      opacity: 1,
      y: 0,
      duration: 0.9,
      ease: 'power3.out',
    },
    0.15
  )

  // Animación del subtítulo - más sutil
  tl.fromTo(
    subtitleRef.value,
    {
      opacity: 0,
      y: isMobile() ? 15 : 20,
    },
    {
      opacity: 1,
      y: 0,
      duration: 0.8,
      ease: 'power2.out',
    },
    0.3
  )

  // Animación de botones - fade in con stagger
  tl.fromTo(
    buttonsRef.value?.querySelectorAll('button'),
    {
      opacity: 0,
      y: isMobile() ? 12 : 20,
    },
    {
      opacity: 1,
      y: 0,
      duration: 0.7,
      ease: 'power2.out',
      stagger: 0.08,
    },
    0.45
  )

  // Animación del trust indicator
  tl.fromTo(
    trustRef.value,
    {
      opacity: 0,
      y: isMobile() ? 10 : 15,
    },
    {
      opacity: 1,
      y: 0,
      duration: 0.7,
      ease: 'power2.out',
    },
    0.6
  )

  // Hover animations para botones - solo en desktop
  if (!isMobile()) {
    const buttons = buttonsRef.value?.querySelectorAll('button')
    buttons?.forEach((button) => {
      button.addEventListener('mouseenter', () => {
        gsap.to(button, {
          scale: 1.03,
          duration: 0.3,
          ease: 'power2.out',
        })
      })
      button.addEventListener('mouseleave', () => {
        gsap.to(button, {
          scale: 1,
          duration: 0.3,
          ease: 'power2.out',
        })
      })
    })
  }
})

onUnmounted(() => {
  // Limpiar animaciones
  gsap.killTweensOf([badgeRef.value, titleRef.value, subtitleRef.value, buttonsRef.value, trustRef.value])
})
</script>

<style scoped>
.hero-bg {
  position: relative;
  overflow: hidden;
  min-height: 100vh;
}

/* Fade inferior */
.hero-bg::after {
  content: '';
  position: absolute;
  left: 0;
  right: 0;
  bottom: 0;
  height: 120px;

  background: linear-gradient(
    to bottom,
    rgba(255, 255, 255, 0) 0%,
    rgba(255, 255, 255, 0.6) 40%,
    #f9fafb 100%
  );

  pointer-events: none;
  z-index: 5;
}
</style>

<template>
  <section
    id="home"
    class="hero-bg flex items-center justify-center px-4 sm:px-6 lg:px-8 relative"
  >

    <!-- BACKGROUND -->
    <div ref="sectionRef" class="absolute inset-0 z-10 opacity-35">
      <LiquidEther
        class="w-full h-full"
        :colors="['#0128EC', '#1F4CFF', '#5A7BFF']"
        :mouseForce="20"
        :cursorSize="120"
        :isViscous="false"
        :resolution="0.6"
        :autoDemo="true"
        :autoSpeed="0.4"
        :autoIntensity="1.8"
        :takeoverDelay="0.25"
        :autoResumeDelay="3000"
        :autoRampDuration="0.6"
      />
    </div>

    <!-- CONTENIDO -->
    <div class="max-w-5xl mx-auto text-center relative z-20 pointer-events-none">

      <div ref="badgeRef" class="inline-flex items-center bg-white/20 border border-blue-100 rounded-full px-6 py-2 mb-8 backdrop-blur-md">
        <div class="w-2 h-2 bg-primary rounded-full mr-2"></div>
        <span class="text-secondary font-semibold text-sm">
          Broker en seguros logísticos
        </span>
      </div>

      <h1 ref="titleRef" class="text-5xl md:text-7xl font-bold text-secondary mb-6 font-secondary">
        Seguros para
        <span class="text-primary font-secondary">tu logística</span>
      </h1>

      <p ref="subtitleRef" class="text-xl md:text-2xl text-secondary mb-10 max-w-3xl mx-auto opacity-80 font-secondary">
        Protección integral para empresas de transporte. Cotizaciones rápidas, sin complicaciones.
      </p>

      <div ref="buttonsRef" class="flex flex-col sm:flex-row gap-4 justify-center mb-16 sm:w-auto w-fit mx-auto pointer-events-auto">
        <button class="bg-primary text-white px-6 py-2 rounded-full font-semibold text-sm hover:shadow-lg transition-all duration-300 sm:px-6 px-4 whitespace-nowrap">
          Cotizar ahora
        </button>
        <button class="bg-white/20 border border-white/40 text-secondary px-6 py-2 rounded-full font-semibold text-sm backdrop-blur-md hover:bg-white/30 transition-all duration-300 sm:px-6 px-4 whitespace-nowrap">
          Conocer más
        </button>
      </div>

      <div ref="trustRef" class="text-sm text-secondary opacity-70">
        ✓ Confían más de 50 empresas logísticas
      </div>

    </div>
  </section>
</template>
