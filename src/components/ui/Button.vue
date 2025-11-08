<template>
  <component
    :is="componentType"
    :href="href"
    :class="combinedClasses"
    v-bind="$attrs"
  >
    <slot />
  </component>
</template>

<script setup lang="ts">
import { computed } from 'vue';

interface ButtonProps {
  variant?: 'primary' | 'secondary' | 'outline';
  size?: 'sm' | 'md' | 'lg';
  href?: string;
}

const props = withDefaults(defineProps<ButtonProps>(), {
  variant: 'primary',
  size: 'md',
});

// Inherit attributes like disabled, type, etc.
defineOptions({
  inheritAttrs: false,
});

const componentType = computed(() => props.href ? 'a' : 'button');

const baseStyles = "inline-flex items-center justify-center font-bold transition-all duration-300 rounded-lg focus:outline-none focus:ring-2 focus:ring-offset-2 focus:ring-offset-(--deep-black)";

const variants = {
  primary: "bg-gradient-to-r from-(--electric-yellow) to-(--electric-orang) text-(--deep-black) hover:brightness-110 hover:scale-105 focus:ring-(--electric-yellow) shadow-lg shadow-(--electric-yellow)/20",
  secondary: "bg-dark-gray text-white hover:bg-white/10 focus:ring-white/50",
  outline: "border-2 border-(--electric-yellow) text-(--electric-yellow) hover:bg-(--electric-yellow)/10 focus:ring-(--electric-yellow)",
};

const sizes = {
  sm: "px-4 py-2 text-sm",
  md: "px-6 py-3 text-base",
  lg: "px-8 py-4 text-lg",
};

const combinedClasses = computed(() => {
  return `${baseStyles} ${variants[props.variant]} ${sizes[props.size]}`;
});
</script>