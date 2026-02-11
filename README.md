# Bacss - Vue 3 + Tailwind CSS + GSAP

Proyecto base con todas las dependencias configuradas y lista para usar.

## 📦 Dependencias Instaladas

- **Vue 3** (Composition API) - Framework UI progresivo
- **JavaScript ES2022+** - Sintaxis moderna
- **Tailwind CSS v4** - Framework CSS utilities-first
- **GSAP** - Librería de animaciones avanzadas
- **Phosphor Icons** - Conjunto de iconos SVG
- **Vite** - Build tool ultrarrápido
- **PostCSS** - Procesador de CSS
- **Autoprefixer** - Prefijos automáticos de CSS

## 🚀 Primeros Pasos

### Instalación
Las dependencias ya están instaladas. Si necesitas instalarlas de nuevo:

```bash
npm install
```

### Desarrollo
Inicia el servidor de desarrollo:

```bash
npm run dev
```

El servidor estará disponible en `http://localhost:5173` (o el puerto disponible mostrado).

### Build para Producción
```bash
npm build
```

### Preview de Build
```bash
npm run preview
```

## 📁 Estructura del Proyecto

```
src/
├── main.js           # Bootstrap de la aplicación
├── App.vue           # Componente raíz
├── style.css         # Estilos globales (Tailwind)
├── components/
│   ├── BaseButton.vue    # Botón reutilizable
│   ├── BaseIcon.vue      # Wrapper de iconos Phosphor
│   └── HelloWorld.vue    # Componente de ejemplo
├── composables/      # Lógica reutilizable (por crear)
├── pages/            # Vistas/páginas (por crear)
├── stores/           # Estado global (por crear)
└── services/         # Llamadas API (por crear)
```

## 🎨 Tailwind CSS

### Configuración
- **tailwind.config.js** - Configuración de temas y extensiones
- **postcss.config.js** - Configuración de PostCSS

### Variables de Color (CSS)
```css
--color-primary: #3b82f6    /* Azul */
--color-secondary: #1e293b  /* Slate */
--color-accent: #ec4899     /* Pink */
```

### Uso en Componentes
```vue
<div class="bg-primary text-white p-4 rounded-lg">
  Contenido con Tailwind
</div>
```

## 🎭 Phosphor Icons

### Uso Básico
Los iconos de Phosphor Icons v2 para Vue 3 utilizan el prefijo `Ph`:

```vue
<script setup>
import { PhHeart, PhStar, PhRocket } from '@phosphor-icons/vue'
</script>

<template>
  <PhHeart :size="24" weight="bold" color="red" />
</template>
```

**Nota:** Todos los nombres de iconos tienen el prefijo `Ph` (ej: `PhHeart`, `PhStar`, `PhRocket`)

### Con BaseIcon Component
```vue
<script setup>
import BaseIcon from '@/components/BaseIcon.vue'
import { PhHeart } from '@phosphor-icons/vue'
</script>

<template>
  <BaseIcon :icon="PhHeart" size="24" weight="bold" color="red" />
</template>
```

## ✨ GSAP (Animaciones)

### Ejemplo Básico
```javascript
import gsap from 'gsap'

gsap.to('.element', {
  duration: 1,
  opacity: 0,
  y: -20,
  ease: 'power2.out'
})
```

### Con Vue 3 (Composition API)
```vue
<script setup>
import { onMounted, ref } from 'vue'
import gsap from 'gsap'

const boxRef = ref(null)

onMounted(() => {
  gsap.from(boxRef.value, {
    opacity: 0,
    y: 50,
    duration: 0.5
  })
})
</script>

<template>
  <div ref="boxRef" class="box">Animado</div>
</template>
```

## 🛠️ Componentes Base

### BaseButton
Botón reutilizable con variantes.

```vue
<BaseButton variant="primary" size="md" @click="handleClick">
  Click me
</BaseButton>
```

**Props:**
- `variant`: 'primary' | 'secondary' | 'danger' (default: 'primary')
- `size`: 'sm' | 'md' | 'lg' (default: 'md')
- `disabled`: boolean (default: false)

### BaseIcon
Wrapper para iconos Phosphor con props consistentes.

```vue
<BaseIcon 
  :icon="Heart"
  size="24"
  weight="bold"
  color="currentColor"
/>
```

**Props:**
- `icon`: Componente de icono (required)
- `size`: número o string (default: 24)
- `weight`: 'thin' | 'light' | 'regular' | 'bold' | 'fill' | 'duotone' (default: 'regular')
- `color`: CSS color value (default: 'currentColor')

## 📝 Convenciones

### Nombrado de Componentes
- **Componentes Base**: `Base*.vue` (ej: `BaseButton.vue`)
- **Componentes UI**: Nombre descriptivo (ej: `UserCard.vue`)
- **Páginas**: `*Page.vue` (ej: `HomePage.vue`)

### Estructura de Componentes
1. **Script** con props, emits, y lógica
2. **Template** con estructura
3. **Style** scoped si es necesario (preferir Tailwind)

### Composables
Siempre prefixen con `use` (ej: `useUserData.js`)

## 🔗 Recursos

- [Vue 3 Docs](https://vuejs.org/)
- [Tailwind CSS Docs](https://tailwindcss.com/)
- [GSAP Docs](https://greensock.com/gsap/)
- [Phosphor Icons](https://phosphoricons.com/)
- [Vite Docs](https://vitejs.dev/)

## 📋 Checklist para Nuevas Features

- [ ] Componentes siguen Single Responsibility Principle
- [ ] Lógica extraída a composables
- [ ] Tests escritos (si es necesario)
- [ ] Sin errores de linting
- [ ] Tailwind CSS utilizado para estilos
- [ ] Documentación actualizada

¡Listo para empezar a construir! 🎉
