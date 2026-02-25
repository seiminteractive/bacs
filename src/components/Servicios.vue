<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import {
  PhTruck,
  PhPackage,
  PhShieldCheckered,
  PhCurrencyDollar,
} from '@phosphor-icons/vue'
import SolutionCard from './SolutionCard.vue'

gsap.registerPlugin(ScrollTrigger)

/**
 * Servicios - Sección de servicios/productos
 * 
 * Responsabilidad: Orquestar visualización de servicios
 * Con animaciones premium al scroll
 */

const sectionRef = ref(null)
const labelRef = ref(null)
const titleRef = ref(null)
const descriptionRef = ref(null)
const cardsContainerRef = ref(null)

// Detectar si es mobile
const isMobile = () => window.innerWidth < 768

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

onMounted(() => {
  // Timeline para header
  const headerTl = gsap.timeline({
    scrollTrigger: {
      trigger: sectionRef.value,
      start: 'top 65%',
      toggleActions: 'play none none reverse',
    },
  })

  // Label - fade in con movimiento
  headerTl.fromTo(
    labelRef.value,
    {
      opacity: 0,
      x: isMobile() ? -10 : -15,
    },
    {
      opacity: 1,
      x: 0,
      duration: 0.6,
      ease: 'power2.out',
    },
    0
  )

  // Título - fade in con movimiento hacia arriba
  headerTl.fromTo(
    titleRef.value,
    {
      opacity: 0,
      y: isMobile() ? 20 : 30,
    },
    {
      opacity: 1,
      y: 0,
      duration: 0.8,
      ease: 'power3.out',
    },
    0.1
  )

  // Descripción - fade in suave
  headerTl.fromTo(
    descriptionRef.value,
    {
      opacity: 0,
      y: isMobile() ? 12 : 16,
    },
    {
      opacity: 1,
      y: 0,
      duration: 0.7,
      ease: 'power2.out',
    },
    0.25
  )

  // Cards - fade in con stagger elegante
  setTimeout(() => {
    const cards = cardsContainerRef.value?.querySelectorAll('[data-service-card]')
    if (cards && cards.length > 0) {
      gsap.fromTo(
        cards,
        {
          opacity: 0,
          y: isMobile() ? 20 : 30,
        },
        {
          opacity: 1,
          y: 0,
          duration: 0.6,
          ease: 'power2.out',
          stagger: {
            amount: 0.3, // Total duration para todas las cards
            from: 'start',
          },
          scrollTrigger: {
            trigger: cardsContainerRef.value,
            start: 'top 70%',
            toggleActions: 'play none none reverse',
          },
        }
      )
    }
  }, 100)

  // Hover effects en cards (solo desktop)
  if (!isMobile()) {
    setTimeout(() => {
      const cards = cardsContainerRef.value?.querySelectorAll('[data-service-card]')
      cards?.forEach((card) => {
        card.addEventListener('mouseenter', () => {
          gsap.to(card, {
            y: -12,
            boxShadow: '0 24px 48px rgba(0, 0, 0, 0.12)',
            duration: 0.3,
            ease: 'power2.out',
          })
        })
        card.addEventListener('mouseleave', () => {
          gsap.to(card, {
            y: 0,
            boxShadow: '0 4px 12px rgba(0, 0, 0, 0.05)',
            duration: 0.3,
            ease: 'power2.out',
          })
        })
      })
    }, 150)
  }
})

onUnmounted(() => {
  ScrollTrigger.getAll().forEach(trigger => trigger.kill())
})
</script>

<template>
  <section ref="sectionRef" id="servicios" class="py-20 md:py-32 px-4 sm:px-6 lg:px-8 bg-gray-50 relative overflow-hidden">
    <!-- Decoración de fondo - Degradados sutiles (fuera del area visible) -->
    <!-- <div class="absolute top-0 -right-96 w-96 h-96 bg-blue-100 rounded-full blur-3xl opacity-15 -z-10"></div>
    <div class="absolute -bottom-96 -left-96 w-80 h-80 bg-blue-50 rounded-full blur-3xl opacity-20 -z-10"></div> -->
    
    <div class="max-w-7xl mx-auto relative z-10">
      <!-- Header -->
      <div class="text-center mb-16">
        <p ref="labelRef" class="text-sm font-secondary text-primary uppercase tracking-widest mb-4">
          Nuestros Servicios
        </p>
        <h2 ref="titleRef" class="text-4xl md:text-5xl font-bold font-secondary text-secondary mb-4">
          Cobertura Completa
        </h2>
        <p ref="descriptionRef" class="text-xl text-secondary font-secondary max-w-2xl mx-auto opacity-80">
          Soluciones especializadas diseñadas para proteger tu negocio logístico.
        </p>
      </div>

      <!-- Grid de servicios -->
      <div ref="cardsContainerRef" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-6 auto-rows-max">
        <div data-service-card v-for="servicio in servicios" :key="servicio.id" class="h-full">
          <SolutionCard
            :icon="servicio.icon"
            :title="servicio.title"
            :description="servicio.description"
          />
        </div>
      </div>
    </div>
  </section>
</template>
