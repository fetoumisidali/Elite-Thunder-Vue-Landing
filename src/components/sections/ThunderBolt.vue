<script setup lang="ts">
import { ref, onMounted, onUnmounted } from 'vue';

// Define the component's name for debugging (equivalent to the 'name' property)
defineOptions({
  name: 'ThunderBolt'
});

// Define props using TypeScript-based syntax
const props = defineProps<{
  delay: number;      // When to start the animation (milliseconds)
  duration: number;   // How long each flash cycle lasts (milliseconds)
  startX: number;     // Starting X position (relative to offset)
  startY: number;     // Starting Y position (relative to offset)
  endX: number;       // Ending X position (relative to offset)
  endY: number;       // Ending Y position (relative to offset)
  offsetX: number;    // Offset X (center of yellow circle)
  offsetY: number;     // Offset Y (center of yellow circle)
}>();

// This stores the SVG path data for the lightning.
// It's automatically exposed to the template.
const path = ref<string>('');

// This variable will hold the interval ID.
// 'number' is the correct type for setInterval in browsers.
let intervalId: number | null = null;

// FUNCTION: Generate random lightning path
const generateLightning = () => {
  // Start the path at the yellow circle center
  let pathData = `M ${props.startX + props.offsetX} ${props.startY + props.offsetY}`;

  // How many segments in the lightning bolt
  const segments = 10;

  // How much random variation (makes it look jagged)
  const variance = 30;

  // Create jagged lightning path by adding random points
  for (let i = 1; i <= segments; i++) {
    // Calculate progress from start to end (0 to 1)
    const progress = i / segments;

    // Calculate X position with random offset for zigzag effect
    const x = (props.startX + props.offsetX) +
              (props.endX - props.startX) * progress +
              (Math.random() - 0.5) * variance;

    // Calculate Y position (straight line)
    const y = (props.startY + props.offsetY) +
              (props.endY - props.startY) * progress;

    // Add this point to the path
    pathData += ` L ${x} ${y}`;
  }

  // End at the target position
  pathData += ` L ${props.endX + props.offsetX} ${props.endY + props.offsetY}`;

  // Update the path
  path.value = pathData;
};

// When component mounts, start generating lightning
onMounted(() => {
  generateLightning();
  // Regenerate the path every [duration] milliseconds
  intervalId = setInterval(generateLightning, props.duration);
});

// Clean up when component unmounts
onUnmounted(() => {
  if (intervalId) clearInterval(intervalId);
});
</script>

<template>
  <svg
    class="absolute inset-0 w-full h-full pointer-events-none z-10 thunder-flash"
    :style="{
      animationDelay: delay + 'ms',
      animationDuration: duration + 'ms'
    }"
  >
    <defs>
      <filter id="glow">
        <feGaussianBlur stdDeviation="4" result="coloredBlur" />
        <feMerge>
          <feMergeNode in="coloredBlur" />
          <feMergeNode in="SourceGraphic" />
        </feMerge>
      </filter>
    </defs>

    <path
      :d="path"
      stroke="#fbbf24"
      stroke-width="3"
      fill="none"
      filter="url(#glow)"
      stroke-linecap="round"
    />

    <path
      :d="path"
      stroke="#fef3c7"
      stroke-width="1"
      fill="none"
      opacity="0.6"
    />
  </svg>
</template>

<style scoped>
/* This animation is implied by the 'thunder-flash' class and 
  the 'animationDelay'/'animationDuration' props in your original code.
  I've added a basic flash animation to make the component work standalone.
*/
@keyframes thunder-flash-animation {
  0%, 100% { opacity: 0; }
  5%, 50% { opacity: 1; }
  10%, 40% { opacity: 0; }
  15%, 30% { opacity: 1; }
  20% { opacity: 0; }
}

.thunder-flash {
  animation-name: thunder-flash-animation;
  animation-iteration-count: infinite;
  opacity: 0; /* Start invisible until delay */
}
</style>