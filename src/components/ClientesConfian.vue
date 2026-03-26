<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import { Swiper, SwiperSlide } from 'swiper/vue'
import { Autoplay } from 'swiper/modules'
import 'swiper/css'

gsap.registerPlugin(ScrollTrigger)

const sectionRef = ref(null)
const titleRef = ref(null)
const descriptionRef = ref(null)
const swiperRef = ref(null)

const baseClientes = [
  { id: 1, nombre: 'Alba-Caución', logo: '/Alba.png'},
  { id: 2, nombre: 'Allianz', logo: '/Allianz.png'},
  { id: 3, nombre: 'ART-Prevencion-Riesgos', logo: '/ARTprevencion.png'},
  { id: 4, nombre: 'Evolución-Seguros', logo: '/EvolucionSeguros.png'},
  // { id: 5, nombre: 'Galeano-Seguros', logo: '/Galeano.png' },
  // { id: 6, nombre: 'Libra-Seguros', logo: '/Libra.svg'},
  { id: 7, nombre: 'Mercantil-Andina', logo: '/MercantilAndina.png'},
  { id: 8, nombre: 'Nación-Seguros', logo: '/NacionSeguros.png'},
  { id: 9, nombre: 'Premiar-Seguros', logo: '/Premiar.png'},
  { id: 10, nombre: 'Prevención-Salud', logo: '/PrevencionSalud.svg'},
  { id: 11, nombre: 'Provicencia-Seguros', logo: '/Provicencia.png'},
  { id: 12, nombre: 'Rivadavia-Seguros', logo: '/Rivadavia.png'},
  { id: 13, nombre: 'Sancor-Seguros', logo: '/SancorSeguros.png'},
  { id: 14, nombre: 'San-Cristobal-Seguros', logo: '/SanCristobal.png'},
  { id: 15, nombre: 'Triunfo-Seguros', logo: '/TriunfoSeguros.png'},
  // { id: 16, nombre: 'Tutelar-Seguros', logo: '/Tutelar.jpg'},
  { id: 17, nombre: 'Afianzadora-Seguros', logo: '/Afianzadora.jpeg'},
  { id: 18, nombre: 'ProvinciaART-Seguros', logo: '/ProvinciaART.png'},
]

const isMobile = () => window.innerWidth < 768

const swiperModules = [Autoplay]

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
  setTimeout(() => {
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
            amount: 0.4,
            from: 'start',
          },
        },
        0
      )
    }
  }, 100)

  // Hover animations para cards (solo desktop)
  if (!isMobile()) {
    setTimeout(() => {
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
    }, 100)
  }
})

onUnmounted(() => {
  ScrollTrigger.getAll().forEach(trigger => trigger.kill())
})
</script>


<style scoped>
:deep(.swiper) {
  overflow: visible;
  width: 100%;
}

:deep(.swiper-wrapper) {
  transition-timing-function: linear;
}

:deep(.swiper-slide) {
  width: auto;
  display: flex;
  align-items: center;
  justify-content: center;
}

/* Fade gradients en los extremos */
.carousel-container {
  position: relative;
  overflow: hidden;
}

.carousel-container::before {
  content: '';
  position: absolute;
  left: 0;
  top: 0;
  bottom: 0;
  width: 128px;
  background: linear-gradient(to right, rgb(249, 250, 251), transparent);
  z-index: 10;
  pointer-events: none;
}

.carousel-container::after {
  content: '';
  position: absolute;
  right: 0;
  top: 0;
  bottom: 0;
  width: 128px;
  background: linear-gradient(to left, rgb(249, 250, 251), transparent);
  z-index: 10;
  pointer-events: none;
}
</style>

<template>
  <section ref="sectionRef" class="py-20 md:py-24 bg-gray-50 overflow-hidden">
    
    <!-- Header centrado -->
    <div class="max-w-7xl mx-auto px-4 sm:px-6 lg:px-8">
      <div class="text-center mb-12">
        <h2 ref="titleRef" class="text-3xl md:text-4xl font-bold font-secondary text-secondary mb-3">
          Compañías con las que trabajamos
        </h2>
        <p ref="descriptionRef" class="text-lg text-secondary font-secondary max-w-2xl mx-auto">
          Empresas líderes en logística y transporte en toda la región confían en Bacs para su protección.
        </p>
      </div>
    </div>

    <!-- Carousel con Swiper -->
    <div class="carousel-container w-screen left-1/2 right-1/2 -ml-[50vw] -mr-[50vw] py-8 sm:py-12">
      <Swiper
        ref="swiperRef"
        :modules="swiperModules"
        :slides-per-view="'auto'"
        :space-between="isMobile() ? 16 : 32"
        :autoplay="{
          delay: 0,
          disableOnInteraction: false,
          pauseOnMouseEnter: false,
        }"
        :speed="isMobile() ? 3000 : 5000"
        loop
        :grab-cursor="false"
        class="w-full px-4 sm:px-6 lg:px-8"
      >
        <SwiperSlide v-for="cliente in baseClientes" :key="cliente.id">
          <div
            class="client-card
              bg-white rounded-xl p-3 sm:p-6 h-24 sm:h-32 w-32 sm:w-40 lg:w-48
              flex items-center justify-center
              shadow-sm hover:shadow-md transition-all duration-300
              border border-gray-100 hover:border-primary
              group flex-shrink-0
            "
          >
            <img
              :src="cliente.logo"
              :alt="cliente.nombre"
              class="max-w-full max-h-full object-contain opacity-60 group-hover:opacity-100 transition-opacity duration-300"
            />
          </div>
        </SwiperSlide>
      </Swiper>
    </div>

    <!-- Indicador -->
    <div class="text-center mt-8 px-4">
      <p class="text-sm text-secondary font-secondary">
        Confían en nosotros más de 50 empresas en el sector logístico y de transporte
      </p>
    </div>

  </section>
</template>
