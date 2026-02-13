<script setup>
import { ref, computed, onMounted, onUnmounted } from 'vue'
import gsap from 'gsap'
import { ScrollTrigger } from 'gsap/ScrollTrigger'
import { PhEnvelope, PhPhone, PhMapPin } from '@phosphor-icons/vue'

gsap.registerPlugin(ScrollTrigger)

/**
 * Contacto - Sección de contacto y formulario
 * 
 * Responsabilidad: Mostrar información de contacto y formulario con animaciones
 */

const sectionRef = ref(null)
const titleRef = ref(null)
const descriptionRef = ref(null)
const contactCardsRef = ref(null)
const formRef = ref(null)

// Detectar si es mobile
const isMobile = () => window.innerWidth < 768

const formData = ref({
  nombre: '',
  email: '',
  telefono: '',
  empresa: '',
  mensaje: '',
})

const errors = ref({
  nombre: '',
  email: '',
  telefono: '',
  empresa: '',
  mensaje: '',
})

// Validaciones
const validateEmail = (email) => {
  const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
  return re.test(email)
}

const validatePhone = (phone) => {
  const re = /^[+]?[\d\s\-()]{10,}$/
  return re.test(phone)
}

const validateField = (field, value) => {
  errors.value[field] = ''
  
  if (!value.trim()) {
    errors.value[field] = 'Este campo es obligatorio'
    return false
  }

  if (field === 'email' && !validateEmail(value)) {
    errors.value[field] = 'Email inválido'
    return false
  }

  if (field === 'telefono' && !validatePhone(value)) {
    errors.value[field] = 'Teléfono inválido'
    return false
  }

  if (field === 'nombre' && value.length < 3) {
    errors.value[field] = 'El nombre debe tener al menos 3 caracteres'
    return false
  }

  if (field === 'mensaje' && value.length < 10) {
    errors.value[field] = 'El mensaje debe tener al menos 10 caracteres'
    return false
  }

  return true
}

const isFormValid = computed(() => {
  return (
    formData.value.nombre.trim() &&
    formData.value.email.trim() &&
    formData.value.telefono.trim() &&
    formData.value.empresa.trim() &&
    formData.value.mensaje.trim() &&
    validateEmail(formData.value.email) &&
    validatePhone(formData.value.telefono) &&
    formData.value.nombre.length >= 3 &&
    formData.value.mensaje.length >= 10 &&
    !errors.value.nombre &&
    !errors.value.email &&
    !errors.value.telefono &&
    !errors.value.empresa &&
    !errors.value.mensaje
  )
})

const handleSubmit = () => {
  let isValid = true
  isValid &= validateField('nombre', formData.value.nombre)
  isValid &= validateField('email', formData.value.email)
  isValid &= validateField('telefono', formData.value.telefono)
  isValid &= validateField('empresa', formData.value.empresa)
  isValid &= validateField('mensaje', formData.value.mensaje)

  if (!isValid) {
    return
  }

  const mensaje = `
        Estimados,

        Mi nombre es ${formData.value.nombre} y me contacto para solicitar información sobre sus servicios.

        Datos de contacto:
        • Empresa: ${formData.value.empresa}
        • Email: ${formData.value.email}
        • Teléfono: ${formData.value.telefono}

        Consulta:
        ${formData.value.mensaje}

        Quedo atento a su respuesta.
        Muchas gracias.
        `

  const mensajeCodificado = encodeURIComponent(mensaje)
  const numeroWhatsApp = '5491121683226'
  const urlWhatsApp = `https://wa.me/${numeroWhatsApp}?text=${mensajeCodificado}`
  
  window.open(urlWhatsApp, '_blank')
  
  formData.value = {
    nombre: '',
    email: '',
    telefono: '',
    empresa: '',
    mensaje: '',
  }
  errors.value = {
    nombre: '',
    email: '',
    telefono: '',
    empresa: '',
    mensaje: '',
  }
}

const contactInfo = [
  {
    icon: PhPhone,
    titulo: 'Teléfono',
    valor: '+54 9 11 2168-3226',
    href: 'tel:+5491121683226',
  },
  {
    icon: PhEnvelope,
    titulo: 'Email',
    valor: 'cotizaciones@bacsbroker.com',
    href: 'mailto:cotizaciones@bacsbroker.com',
  },
  {
    icon: PhMapPin,
    titulo: 'Ubicación',
    valor: 'LATAM Region',
    href: '#',
  },
]

onMounted(() => {
  // Timeline para header
  const headerTl = gsap.timeline({
    scrollTrigger: {
      trigger: sectionRef.value,
      start: 'top 65%',
      toggleActions: 'play none none reverse',
    },
  })

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
    0
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
    0.15
  )

  // Contact info cards - fade in con stagger
  setTimeout(() => {
    const cards = contactCardsRef.value?.querySelectorAll('[data-contact-card]')
    if (cards && cards.length > 0) {
      gsap.fromTo(
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
          stagger: 0.08,
          scrollTrigger: {
            trigger: contactCardsRef.value,
            start: 'top 75%',
            toggleActions: 'play none none reverse',
          },
        }
      )
    }
  }, 100)

  // Form inputs - fade in con stagger
  setTimeout(() => {
    const inputs = formRef.value?.querySelectorAll('[data-form-input]')
    if (inputs && inputs.length > 0) {
      gsap.fromTo(
        inputs,
        {
          opacity: 0,
          y: isMobile() ? 12 : 16,
        },
        {
          opacity: 1,
          y: 0,
          duration: 0.5,
          ease: 'power2.out',
          stagger: 0.06,
          scrollTrigger: {
            trigger: formRef.value,
            start: 'top 75%',
            toggleActions: 'play none none reverse',
          },
        }
      )
    }
  }, 150)
})

onUnmounted(() => {
  ScrollTrigger.getAll().forEach(trigger => trigger.kill())
})
</script>

<style scoped>
.contact-bg {
  position: relative;
  background: #f7f9ff;
  overflow: hidden;
}

.contact-bg::before {
  content: '';
  position: absolute;
  inset: 0;
  pointer-events: none;

  background:

    /* DERECHA - Azul más claro */
    radial-gradient(
      ellipse 65% 85% at 115% 30%,
      rgba(1, 40, 236, 0.18) 0%,
      rgba(1, 40, 236, 0.10) 35%,
      transparent 70%
    ),

    /* IZQUIERDA - Azul más profundo */
    radial-gradient(
      ellipse 75% 95% at -20% 75%,
      rgba(1, 40, 236, 0.45) 0%,
      rgba(1, 40, 236, 0.28) 30%,
      rgba(1, 40, 236, 0.14) 55%,
      transparent 80%
    );

  filter: blur(110px);
}

.contact-bg::after {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 180px; /* ajustable */

  background: linear-gradient(
    to bottom,
    #ffffff 0%,
    rgba(255, 255, 255, 0.9) 30%,
    rgba(255, 255, 255, 0.6) 55%,
    transparent 100%
  );

  pointer-events: none;
}



@keyframes float {
  0%, 100% {
    transform: translate(0, 0);
  }
  50% {
    transform: translate(30px, -30px);
  }
}

.form-input {
  @apply w-full px-4 py-3 rounded-lg border border-gray-100 bg-white/50 backdrop-blur-sm font-secondary text-secondary placeholder-gray-400 transition-all duration-300;
}

.form-input:focus {
  @apply outline-none border-primary bg-white ring-1 ring-blue-500/20;
}
</style>

<template>
  <section ref="sectionRef" id="contacto" class="contact-bg py-20 md:py-32 px-4 sm:px-6 lg:px-8 relative">
    <div class="max-w-5xl mx-auto relative z-10">
      <!-- Header minimalista -->
      <div class="text-center mb-20">
        <h2 ref="titleRef" class="text-4xl md:text-5xl font-bold font-primary text-secondary mb-3">
          Contacto
        </h2>
        <p ref="descriptionRef" class="text-lg text-secondary/70 font-secondary max-w-2xl mx-auto">
          Tu solución de seguros logísticos está a un mensaje de distancia
        </p>
      </div>

      <div class="grid grid-cols-1 lg:grid-cols-5 gap-16 h-full">
        <!-- Info de contacto minimalista con glassmorphism -->
        <div ref="contactCardsRef" class="lg:col-span-2 space-y-6 flex flex-col justify-start">
          <div
            v-for="info in contactInfo"
            :key="info.titulo"
            data-contact-card
            class="group cursor-pointer"
          >
            <a
              v-if="info.href !== '#'"
              :href="info.href"
              target="_blank"
              class="flex flex-col items-start gap-3 p-5 rounded-xl backdrop-blur-md bg-white/20 border border-white/40 hover:bg-white/30 hover:border-white/60 transition-all duration-300"
            >
              <component
                :is="info.icon"
                :size="24"
                weight="regular"
                color="#0128ec"
                class="group-hover:scale-110 transition-transform duration-300"
              />
              <div>
                <p class="text-xs font-secondary text-secondary/60 mb-1 uppercase tracking-wide">
                  {{ info.titulo }}
                </p>
                <p class="font-primary font-semibold text-secondary text-sm group-hover:text-primary transition-colors">
                  {{ info.valor }}
                </p>
              </div>
            </a>
            <div v-else class="flex flex-col items-start gap-3 p-5 rounded-xl backdrop-blur-md bg-white/20 border border-white/40">
              <component
                :is="info.icon"
                :size="24"
                weight="regular"
                color="#0128ec"
              />
              <div>
                <p class="text-xs font-secondary text-secondary/60 mb-1 uppercase tracking-wide">
                  {{ info.titulo }}
                </p>
                <p class="font-primary font-semibold text-secondary text-sm">
                  {{ info.valor }}
                </p>
              </div>
            </div>
          </div>
        </div>

        <!-- Formulario minimalista -->
        <div class="lg:col-span-3 flex flex-col justify-start">
          <form ref="formRef" @submit.prevent="handleSubmit" class="space-y-5">
            <!-- Nombre y Email en una fila -->
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
              <div data-form-input>
                <label class="text-xs font-secondary text-secondary/70 mb-1 block">Nombre <span class="text-red-500">*</span></label>
                <input
                  v-model="formData.nombre"
                  type="text"
                  placeholder="Tu nombre"
                  class="form-input"
                  @blur="validateField('nombre', formData.nombre)"
                />
                <span v-if="errors.nombre" class="text-xs text-red-500 mt-1 block">{{ errors.nombre }}</span>
              </div>
              <div data-form-input>
                <label class="text-xs font-secondary text-secondary/70 mb-1 block">Email <span class="text-red-500">*</span></label>
                <input
                  v-model="formData.email"
                  type="email"
                  placeholder="tu@email.com"
                  class="form-input"
                  @blur="validateField('email', formData.email)"
                />
                <span v-if="errors.email" class="text-xs text-red-500 mt-1 block">{{ errors.email }}</span>
              </div>
            </div>

            <!-- Teléfono y Empresa en una fila -->
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
              <div data-form-input>
                <label class="text-xs font-secondary text-secondary/70 mb-1 block">Teléfono <span class="text-red-500">*</span></label>
                <input
                  v-model="formData.telefono"
                  type="tel"
                  placeholder="+54 9 11 XXXX-XXXX"
                  class="form-input"
                  @blur="validateField('telefono', formData.telefono)"
                />
                <span v-if="errors.telefono" class="text-xs text-red-500 mt-1 block">{{ errors.telefono }}</span>
              </div>
              <div data-form-input>
                <label class="text-xs font-secondary text-secondary/70 mb-1 block">Empresa <span class="text-red-500">*</span></label>
                <input
                  v-model="formData.empresa"
                  type="text"
                  placeholder="Nombre de tu empresa"
                  class="form-input"
                  @blur="validateField('empresa', formData.empresa)"
                />
                <span v-if="errors.empresa" class="text-xs text-red-500 mt-1 block">{{ errors.empresa }}</span>
              </div>
            </div>

            <!-- Mensaje -->
            <div data-form-input>
              <label class="text-xs font-secondary text-secondary/70 mb-1 block">Mensaje <span class="text-red-500">*</span></label>
              <textarea
                v-model="formData.mensaje"
                placeholder="Tu mensaje (mínimo 10 caracteres)"
                rows="4"
                class="form-input resize-none"
                @blur="validateField('mensaje', formData.mensaje)"
              ></textarea>
              <span v-if="errors.mensaje" class="text-xs text-red-500 mt-1 block">{{ errors.mensaje }}</span>
            </div>

            <!-- Botón minimalista -->
            <button
              type="submit"
              :disabled="!isFormValid"
              class="w-full px-6 py-3 bg-primary text-white font-primary font-semibold text-sm rounded-full transition-all duration-300"
              :class="isFormValid ? 'hover:bg-primary/90 hover:shadow-lg cursor-pointer' : 'opacity-50 cursor-not-allowed bg-gray-400'"
            >
              Enviar
            </button>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>
