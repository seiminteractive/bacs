<script setup>
import { ref } from 'vue'
import { PhEnvelope, PhPhone, PhMapPin } from '@phosphor-icons/vue'

/**
 * Contacto - Sección de contacto y formulario
 * 
 * Responsabilidad: Mostrar información de contacto y formulario
 * Maneja estado local del formulario únicamente
 */

const formData = ref({
  nombre: '',
  email: '',
  telefono: '',
  empresa: '',
  mensaje: '',
})

const handleSubmit = () => {
  // Aquí iría la lógica de envío
  console.log('Formulario enviado:', formData.value)
}

const contactInfo = [
  {
    icon: PhPhone,
    titulo: 'Teléfono',
    valor: '+1 (555) 123-4567',
    href: 'tel:+15551234567',
  },
  {
    icon: PhEnvelope,
    titulo: 'Email',
    valor: 'info@bacs.com',
    href: 'mailto:info@bacs.com',
  },
  {
    icon: PhMapPin,
    titulo: 'Ubicación',
    valor: 'LATAM Region',
    href: '#',
  },
]
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
  <section id="contacto" class="contact-bg py-20 md:py-32 px-4 sm:px-6 lg:px-8 relative">
    <div class="max-w-5xl mx-auto relative z-10">
      <!-- Header minimalista -->
      <div class="text-center mb-20">
        <h2 class="text-4xl md:text-5xl font-bold font-primary text-secondary mb-3">
          Contacto
        </h2>
        <p class="text-lg text-secondary/70 font-secondary max-w-2xl mx-auto">
          Tu solución de seguros logísticos está a un mensaje de distancia
        </p>
      </div>

      <div class="grid grid-cols-1 lg:grid-cols-5 gap-16 h-full">
        <!-- Info de contacto minimalista con glassmorphism -->
        <div class="lg:col-span-2 space-y-6 flex flex-col justify-start">
          <div
            v-for="info in contactInfo"
            :key="info.titulo"
            class="group cursor-pointer"
          >
            <a
              v-if="info.href !== '#'"
              :href="info.href"
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
          <form @submit.prevent="handleSubmit" class="space-y-5">
            <!-- Nombre y Email en una fila -->
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
              <input
                v-model="formData.nombre"
                type="text"
                placeholder="Nombre"
                class="form-input"
              />
              <input
                v-model="formData.email"
                type="email"
                placeholder="Email"
                class="form-input"
              />
            </div>

            <!-- Teléfono y Empresa en una fila -->
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
              <input
                v-model="formData.telefono"
                type="tel"
                placeholder="Teléfono"
                class="form-input"
              />
              <input
                v-model="formData.empresa"
                type="text"
                placeholder="Empresa"
                class="form-input"
              />
            </div>

            <!-- Mensaje -->
            <textarea
              v-model="formData.mensaje"
              placeholder="Tu mensaje"
              rows="4"
              class="form-input resize-none"
            ></textarea>

            <!-- Botón minimalista -->
            <button
              type="submit"
              class="w-full px-6 py-3 bg-primary text-white font-primary font-semibold text-sm rounded-full hover:bg-primary/90 hover:shadow-lg transition-all duration-300"
            >
              Enviar
            </button>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>
