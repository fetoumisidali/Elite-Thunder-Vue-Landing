<template>
  <div 
    class="relative w-full group" 
    :style="componentStyles"
  >
    <div
      v-for="corner in corners"
      :key="corner.position"
      :class="[
        'absolute w-12 h-12 transition-all duration-300',
        'opacity-80 group-hover:opacity-100 group-hover:w-16 group-hover:h-16',
        corner.position,
        corner.border,
        corner.rounded,
        corner.color === 'color1' ? 'border-(--electric-yellow)' : 'border-(--electric-orange)'
      ]"
    ></div>

    <div
      :class="[
        'p-8 transition-all duration-300 group-hover:-translate-y-2 overflow-hidden relative',
        'bg-gradient-to-br from-[#1a1a1a] to-[#151515]',
        'border border-white/5',
        'hover:border-[var(--color-1)]/50', // JIT-safe
        'mx-4 my-4'
      ]"
    >
      <div
        :class="[
          'absolute -inset-px blur-xl transition-opacity duration-500 -z-10',
          'opacity-0 group-hover:opacity-100',
          'bg-gradient-to-br from-[var(--color-1)]/20 to-transparent' // JIT-safe
        ]"
      ></div>

      <div
        :class="[
          'w-14 h-14 rounded-sm flex items-center justify-center mb-6',
          'transition-all duration-300',
          'group-hover:scale-110',
          'bg-[var(--color-1)]/10',     // JIT-safe
          'text-[var(--color-1)]',      // JIT-safe
          'group-hover:bg-[var(--color-1)]', // JIT-safe
          'group-hover:text-black'
        ]"
      >
        <component :is="icon" :size="28" :stroke-width="1.5" />
      </div>

      <h3
        :class="[
          'text-xl font-bold mb-3 transition-colors',
          'text-white',
          'group-hover:text-[var(--color-1)]' // JIT-safe
        ]"
      >
        {{ title }}
      </h3>

      <p class="text-gray-400 leading-relaxed">
        {{ description }}
      </p>
    </div>
  </div>
</template>

<script setup>
import { defineProps, computed } from 'vue';

const props = defineProps({
  icon: {
    type: [Object, Function],
    required: true
  },
  title: {
    type: String,
    required: true
  },
  description: {
    type: String,
    required: true
  },
  // Props are now actual CSS color values
  color1Value: {
    type: String,
    default: '#f59e0b' // Default is yellow-400
  },
  color2Value: {
    type: String,
    default: '#a855f7' // Default is purple-500
  }
});

// Bind prop values to CSS variables for use in the template
const componentStyles = computed(() => ({
  '--color-1': props.color1Value,
  '--color-2': props.color2Value
}));

// Configuration for the v-for loop to generate corners
const corners = [
  { 
    position: 'top-0 left-0', 
    border: 'border-t-6 border-l-6', 
    rounded: 'rounded-tl-lg', 
    color: 'color1' 
  },
  { 
    position: 'top-0 right-0', 
    border: 'border-t-6 border-r-6', 
    rounded: 'rounded-tr-lg', 
    color: 'color2' 
  },
  { 
    position: 'bottom-0 left-0', 
    border: 'border-b-6 border-l-6', 
    rounded: 'rounded-bl-lg', 
    color: 'color2' 
  },
  { 
    position: 'bottom-0 right-0', 
    border: 'border-b-6 border-r-6', 
    rounded: 'rounded-br-lg', 
    color: 'color1' 
  }
];

</script>