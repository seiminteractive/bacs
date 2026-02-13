<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

const sectionRef = ref(null)
const titleRef = ref(null)
const descriptionRef = ref(null)
const cardsRef = ref([])

const clientes = computed(() => {
  const baseClientes = [
    { id: 1, nombre: 'Logística Premium', logo: '../src/assets/img/new-volvo-logo.png' },
    { id: 2, nombre: 'TransExpress Global', logo: '../src/assets/img/new-volvo-logo.png' },
    { id: 3, nombre: 'Fleet Solutions', logo: '../src/assets/img/new-volvo-logo.png' },
    { id: 4, nombre: 'Cargo Express', logo: '../src/assets/img/new-volvo-logo.png' },
    { id: 5, nombre: 'Delivery Network', logo: '../src/assets/img/new-volvo-logo.png' },
    { id: 6, nombre: 'Maritime Logistics', logo: '../src/assets/img/new-volvo-logo.png' },
  ]

  return [...baseClientes, ...baseClientes]
})

// Detectar si es mobile
const isMobile = () => window.innerWidth < 768

onMounted(() => {
  // Animación del título y descripción al hacer scroll
  const headerTl = gsap.timeline({
    scrollTrigger: {
      trigger: sectionRef.value,
      start: 'top 70%',
      toggleActions: 'play none none reverse',
    },
  })

  // Título fade in + movimiento hacia arriba
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
      ease: 'power2.out',
    },
    0
  )

  // Descripción fade in + movimiento suave
  headerTl.fromTo(
    descriptionRef.value,
    {
      opacity: 0,
      y: isMobile() ? 15 : 20,
    },
    {
      opacity: 1,
      y: 0,
      duration: 0.7,
      ease: 'power2.out',
    },
    0.15
  )

  // Animación de las cards con stagger elegante
  const cards = document.querySelectorAll('.client-card')
  if (cards.length > 0) {
    const cardsTl = gsap.timeline({
      scrollTrigger: {
        trigger: sectionRef.value,
        start: 'top 65%',
        toggleActions: 'play none none reverse',
      },
    })

    cardsTl.fromTo(
      cards,
      {
        opacity: 0,
        y: isMobile() ? 15 : 25,
      },
      {
        opacity: 1,
        y: 0,
        duration: 0.6,
        ease: 'power2.out',
        stagger: {
          amount: 0.4, // Total duration para todas las cards
          from: 'start',
        },
      },
      0
    )
  }

  // Hover animations para cards (solo desktop)
  if (!isMobile()) {
    const cards = document.querySelectorAll('.client-card')
    cards.forEach((card) => {
      card.addEventListener('mouseenter', () => {
        gsap.to(card, {
          y: -8,
          boxShadow: '0 20px 40px rgba(0, 0, 0, 0.1)',
          duration: 0.3,
          ease: 'power2.out',
        })
      })
      card.addEventListener('mouseleave', () => {
        gsap.to(card, {
          y: 0,
          boxShadow: '0 4px 6px rgba(0, 0, 0, 0.05)',
          duration: 0.3,
          ease: 'power2.out',
        })
      })
    })
  }
})

onUnmounted(() => {
  ScrollTrigger.getAll().forEach(trigger => trigger.kill())
})
</script>


<style scoped>
@keyframes scroll-left {
  from {
    transform: translateX(0);
  }
  to {
    transform: translateX(-50%);
  }
}

/* 📱 MOBILE (más rápido y fluido) */
.carousel-wrapper {
  animation: scroll-left 15s linear infinite;
  will-change: transform;
}

/* 💻 DESKTOP (NO se modifica tu velocidad original) */
@media (min-width: 640px) {
  .carousel-wrapper {
    animation: scroll-left 50s linear infinite;
  }
}

</style>

<template>
  <section ref="sectionRef" class="py-20 md:py-24 bg-gray-50 overflow-hidden">
    
    <!-- Header centrado -->
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="text-center mb-12">
        <h2 ref="titleRef" class="text-3xl md:text-4xl font-bold font-primary text-secondary mb-3">
          Clientes que confían en nosotros
        </h2>
        <p ref="descriptionRef" class="text-lg text-secondary font-secondary max-w-2xl mx-auto">
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
      <div class="carousel-wrapper flex gap-4 sm:gap-8 px-4 sm:px-6 lg:px-8 py-8 sm:py-12">
        <div v-for="(cliente, index) in clientes" :key="cliente.id + '-' + index" class="flex-shrink-0 w-32 sm:w-1/2 lg:w-1/4 xl:w-1/6">

          <div
            class="client-card
              bg-white rounded-xl p-3 sm:p-6 h-24 sm:h-32
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
