<script setup>
import { ref, onMounted, onUnmounted } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'

gsap.registerPlugin(ScrollTrigger)

/**
 * Nosotros - Sección sobre la empresa
 * 
 * Responsabilidad: Comunicar la propuesta de valor, experiencia y especialización
 * Con animaciones premium al scroll
 */

const sectionRef = ref(null)
const labelRef = ref(null)
const titleRef = ref(null)
const textRefs = ref([])
const statsRef = ref(null)
const imageRef = ref(null)

// Detectar si es mobile
const isMobile = () => window.innerWidth < 768

onMounted(() => {
  // Timeline para contenido de texto
  const textTl = gsap.timeline({
    scrollTrigger: {
      trigger: sectionRef.value,
      start: 'top 60%',
      toggleActions: 'play none none reverse',
    },
  })

  // Label "Sobre nosotros" - fade in con movimiento suave
  textTl.fromTo(
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
  textTl.fromTo(
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

  // Párrafos - fade in con stagger
  textTl.fromTo(
    textRefs.value,
    {
      opacity: 0,
      y: isMobile() ? 12 : 16,
    },
    {
      opacity: 1,
      y: 0,
      duration: 0.6,
      ease: 'power2.out',
      stagger: 0.08,
    },
    0.25
  )

  // Stats - fade in y counter animation
  const stats = statsRef.value?.querySelectorAll('.stat-item')
  if (stats) {
    const statsTl = gsap.timeline({
      scrollTrigger: {
        trigger: statsRef.value,
        start: 'top 70%',
        toggleActions: 'play none none reverse',
      },
    })

    statsTl.fromTo(
      stats,
      {
        opacity: 0,
        y: isMobile() ? 10 : 15,
      },
      {
        opacity: 1,
        y: 0,
        duration: 0.6,
        ease: 'power2.out',
        stagger: 0.1,
      },
      0
    )
  }

  // Imagen - fade in con scale sutil
  gsap.fromTo(
    imageRef.value,
    {
      opacity: 0,
      y: isMobile() ? 20 : 40,
      scale: isMobile() ? 0.95 : 0.92,
    },
    {
      opacity: 1,
      y: 0,
      scale: 1,
      duration: 0.9,
      ease: 'power2.out',
      scrollTrigger: {
        trigger: sectionRef.value,
        start: 'top 55%',
        toggleActions: 'play none none reverse',
      },
    }
  )

  // Hover effect en imagen (solo desktop)
  if (!isMobile() && imageRef.value) {
    imageRef.value.addEventListener('mouseenter', () => {
      gsap.to(imageRef.value, {
        y: -12,
        boxShadow: '0 30px 60px rgba(0, 0, 0, 0.15)',
        duration: 0.4,
        ease: 'power2.out',
      })
    })

    imageRef.value.addEventListener('mouseleave', () => {
      gsap.to(imageRef.value, {
        y: 0,
        boxShadow: '0 20px 40px rgba(0, 0, 0, 0.1)',
        duration: 0.4,
        ease: 'power2.out',
      })
    })
  }
})

onUnmounted(() => {
  ScrollTrigger.getAll().forEach(trigger => trigger.kill())
})
</script>

<template>
  <section ref="sectionRef" id="nosotros" class="py-20 md:py-32 px-4 sm:px-6 lg:px-8 bg-white relative overflow-hidden">
    <!-- Decoración de fondo - Degradados sutiles -->
    <div class="absolute top-20 left-0 w-96 h-96 bg-blue-100 rounded-full blur-3xl opacity-15 -z-10"></div>
    <div class="absolute bottom-0 right-0 w-80 h-80 bg-blue-50 rounded-full blur-3xl opacity-20 -z-10"></div>
    
    <div class="max-w-6xl mx-auto relative z-10">
      <div class="grid grid-cols-1 md:grid-cols-2 gap-12 lg:gap-16 items-center">
        <!-- Contenido -->
        <div class="md:text-left text-center">
          <p ref="labelRef" class="text-sm font-secondary text-primary uppercase tracking-widest mb-4 md:text-left text-center">
            Sobre nosotros
          </p>
          <h2 ref="titleRef" class="text-4xl md:text-5xl font-bold font-primary text-secondary mb-6 leading-tight">
            Seguros diseñados por expertos
          </h2>
          <p ref="textRefs" class="text-lg text-secondary font-secondary mb-6 leading-relaxed opacity-80">
            Somos especialistas en seguros para empresas logísticas y de transporte. Con más de 15 años de experiencia, entendemos los desafíos únicos del sector.
          </p>
          <p :ref="el => textRefs.push(el)" class="text-lg text-secondary font-secondary mb-8 leading-relaxed opacity-80">
            Nuestra misión es simple: ofrecer protección integral con procesos transparentes, cotizaciones rápidas y un equipo siempre disponible.
          </p>
          
          <!-- Stats -->
          <div ref="statsRef" class="grid grid-cols-3 gap-8 pt-8 border-t border-gray-100">
            <div class="stat-item text-center md:text-left">
              <div class="text-3xl font-bold text-primary font-primary">50+</div>
              <p class="text-sm text-secondary font-secondary opacity-70 mt-2">Empresas protegidas</p>
            </div>
            <div class="stat-item text-center md:text-left">
              <div class="text-3xl font-bold text-primary font-primary">15+</div>
              <p class="text-sm text-secondary font-secondary opacity-70 mt-2">Años de expertise</p>
            </div>
            <div class="stat-item text-center md:text-left">
              <div class="text-3xl font-bold text-primary font-primary">24/7</div>
              <p class="text-sm text-secondary font-secondary opacity-70 mt-2">Soporte disponible</p>
            </div>
          </div>
        </div>

        <!-- Imagen visual -->
        <div ref="imageRef" class="relative">
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
