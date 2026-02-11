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

<template>
  <section id="contacto" class="py-20 md:py-32 px-4 sm:px-6 lg:px-8 bg-gradient-to-b from-white to-gray-50">
    <div class="max-w-6xl mx-auto">
      <!-- Header -->
      <div class="text-center mb-16">
        <p class="text-sm font-secondary text-primary uppercase tracking-widest mb-4">
          Contáctanos
        </p>
        <h2 class="text-4xl md:text-5xl font-bold font-primary text-secondary mb-4">
          Hablemos de tu negocio
        </h2>
        <p class="text-xl text-secondary font-secondary max-w-2xl mx-auto opacity-80">
          Nuestro equipo está listo para diseñar la solución perfecta para ti.
        </p>
      </div>

      <div class="grid grid-cols-1 lg:grid-cols-3 gap-12">
        <!-- Información de contacto -->
        <div class="lg:col-span-1 space-y-6">
          <div
            v-for="info in contactInfo"
            :key="info.titulo"
          >
            <a
              v-if="info.href !== '#'"
              :href="info.href"
              class="flex items-start gap-4 group cursor-pointer"
            >
              <div class="flex-shrink-0">
                <component
                  :is="info.icon"
                  :size="32"
                  weight="regular"
                  :color="'#0128ec'"
                  class="group-hover:scale-110 transition-transform duration-300"
                />
              </div>
              <div>
                <p class="font-secondary text-sm text-secondary opacity-70 mb-1">
                  {{ info.titulo }}
                </p>
                <p class="font-primary font-bold text-secondary group-hover:text-primary transition-colors">
                  {{ info.valor }}
                </p>
              </div>
            </a>
            <div v-else class="flex items-start gap-4">
              <div class="flex-shrink-0">
                <component
                  :is="info.icon"
                  :size="32"
                  weight="regular"
                  :color="'#0128ec'"
                />
              </div>
              <div>
                <p class="font-secondary text-sm text-secondary opacity-70 mb-1">
                  {{ info.titulo }}
                </p>
                <p class="font-primary font-bold text-secondary">
                  {{ info.valor }}
                </p>
              </div>
            </div>
          </div>
        </div>

        <!-- Formulario -->
        <div class="lg:col-span-2">
          <form @submit.prevent="handleSubmit" class="space-y-6">
            <!-- Nombre -->
            <div>
              <label class="block text-sm font-secondary text-secondary mb-2">
                Nombre
              </label>
              <input
                v-model="formData.nombre"
                type="text"
                placeholder="Tu nombre"
                class="w-full px-4 py-3 rounded-lg border border-gray-200 font-secondary text-secondary placeholder-gray-400 focus:outline-none focus:border-primary focus:ring-1 focus:ring-primary transition-colors"
              />
            </div>

            <!-- Email -->
            <div>
              <label class="block text-sm font-secondary text-secondary mb-2">
                Email
              </label>
              <input
                v-model="formData.email"
                type="email"
                placeholder="tu@empresa.com"
                class="w-full px-4 py-3 rounded-lg border border-gray-200 font-secondary text-secondary placeholder-gray-400 focus:outline-none focus:border-primary focus:ring-1 focus:ring-primary transition-colors"
              />
            </div>

            <!-- Teléfono y Empresa en una fila -->
            <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
              <div>
                <label class="block text-sm font-secondary text-secondary mb-2">
                  Teléfono
                </label>
                <input
                  v-model="formData.telefono"
                  type="tel"
                  placeholder="+1 (555) 000-0000"
                  class="w-full px-4 py-3 rounded-lg border border-gray-200 font-secondary text-secondary placeholder-gray-400 focus:outline-none focus:border-primary focus:ring-1 focus:ring-primary transition-colors"
                />
              </div>
              <div>
                <label class="block text-sm font-secondary text-secondary mb-2">
                  Empresa
                </label>
                <input
                  v-model="formData.empresa"
                  type="text"
                  placeholder="Nombre de tu empresa"
                  class="w-full px-4 py-3 rounded-lg border border-gray-200 font-secondary text-secondary placeholder-gray-400 focus:outline-none focus:border-primary focus:ring-1 focus:ring-primary transition-colors"
                />
              </div>
            </div>

            <!-- Mensaje -->
            <div>
              <label class="block text-sm font-secondary text-secondary mb-2">
                Mensaje
              </label>
              <textarea
                v-model="formData.mensaje"
                placeholder="Cuéntanos más sobre tu negocio..."
                rows="5"
                class="w-full px-4 py-3 rounded-lg border border-gray-200 font-secondary text-secondary placeholder-gray-400 focus:outline-none focus:border-primary focus:ring-1 focus:ring-primary transition-colors resize-none"
              ></textarea>
            </div>

            <!-- Botón -->
            <button
              type="submit"
              class="w-full bg-primary text-white px-6 py-4 rounded-lg font-primary font-bold text-lg hover:shadow-xl hover:scale-105 transition-all duration-300"
            >
              Enviar Mensaje
            </button>
          </form>
        </div>
      </div>
    </div>
  </section>
</template>
