<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import {
  PhMagnifyingGlass,
  PhCheckCircle,
  PhCreditCard,
  PhThumbsUp,
} from '@phosphor-icons/vue'

gsap.registerPlugin(ScrollTrigger)

/**
 * ComoTrabajamos - Sección del proceso
 * 
 * Responsabilidad: Mostrar el flujo de trabajo paso a paso con animaciones premium
 */

const sectionRef = ref(null)
const labelRef = ref(null)
const titleRef = ref(null)
const descriptionRef = ref(null)
const stepsContainerRef = ref(null)

// Detectar si es mobile
const isMobile = () => window.innerWidth < 768

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

  // Pasos - fade in con stagger elegante
  setTimeout(() => {
    const steps = stepsContainerRef.value?.querySelectorAll('[data-step]')
    if (steps && steps.length > 0) {
      gsap.fromTo(
        steps,
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
            amount: 0.4, // Total duration para todos los pasos
            from: 'start',
          },
          scrollTrigger: {
            trigger: stepsContainerRef.value,
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
      const cards = stepsContainerRef.value?.querySelectorAll('[data-step]')
      cards?.forEach((card) => {
        card.addEventListener('mouseenter', () => {
          gsap.to(card, {
            y: -8,
            duration: 0.3,
            ease: 'power2.out',
          })
        })
        card.addEventListener('mouseleave', () => {
          gsap.to(card, {
            y: 0,
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
  <section ref="sectionRef" id="como-trabajamos" class="py-20 md:py-32 px-4 sm:px-6 lg:px-8 bg-white relative overflow-hidden">
    <!-- Decoración de fondo - Degradados sutiles (fuera del area visible) -->
    <div class="absolute -top-96 -left-96 w-96 h-96 bg-blue-100 rounded-full blur-3xl opacity-15 -z-10"></div>
    <div class="absolute -bottom-96 -right-96 w-96 h-96 bg-blue-50 rounded-full blur-3xl opacity-20 -z-10"></div>
    
    <div class="max-w-6xl mx-auto relative z-10">
      <!-- Header -->
      <div class="text-center mb-16">
        <p ref="labelRef" class="text-sm font-secondary text-primary uppercase tracking-widest mb-4">
          Proceso Simple
        </p>
        <h2 ref="titleRef" class="text-4xl md:text-5xl font-bold font-primary text-secondary mb-4">
          Cómo Trabajamos
        </h2>
        <p ref="descriptionRef" class="text-xl text-secondary font-secondary max-w-2xl mx-auto opacity-80">
          Un proceso claro y directo, diseñado para tu comodidad.
        </p>
      </div>

      <!-- Grid de pasos -->
      <div ref="stepsContainerRef" class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-4 gap-8 lg:auto-rows-fr">
        <div
          v-for="(paso, index) in pasos"
          :key="paso.numero"
          data-step
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
