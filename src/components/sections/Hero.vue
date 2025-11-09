<script setup lang="ts">
import { Zap } from 'lucide-vue-next';
import ThunderBolt from './ThunderBolt.vue';
import { ref, onMounted, onUnmounted } from 'vue';

const controllerContainer = ref<HTMLElement>()
const controllerPos = ref({ x: 0, y: 0 });



const thunderBolts = [
  { delay: 0, duration: 2000, startX: 0, startY: 0, endX: -300, endY: -200 },
  { delay: 400, duration: 1800, startX: 0, startY: 0, endX: -200, endY: 250 },
  { delay: 800, duration: 2200, startX: 0, startY: 0, endX: 250, endY: -180 },
  { delay: 1200, duration: 1900, startX: 0, startY: 0, endX: 280, endY: 220 },
  { delay: 1600, duration: 2100, startX: 0, startY: 0, endX: 100, endY: -280 },
  { delay: 600, duration: 2000, startX: 0, startY: 0, endX: -100, endY: 280 }
];

const updatePosition = () => {
  if (controllerContainer.value) {
    const rect = controllerContainer.value.getBoundingClientRect();
    controllerPos.value = {
      x: rect.left + rect.width / 2,
      y: rect.top + rect.height / 2
    };

  }
};
onMounted(() => {
  updatePosition();
  setTimeout(updatePosition, 100);
  setTimeout(updatePosition, 500);

  window.addEventListener('resize', updatePosition);

  const img = controllerContainer.value?.querySelector('img');
  if (img) {
    img.addEventListener('load', updatePosition);
  }
})

onUnmounted(() => {
  window.removeEventListener('resize', updatePosition);
});

</script>

<template>
  <section class="min-h-screen py-20 flex items-center">
    <ThunderBolt v-for="(bolt, index) in thunderBolts" :key="index" :delay="bolt.delay" :duration="bolt.duration"
      :start-x="bolt.startX" :start-y="bolt.startY" :end-x="bolt.endX" :end-y="bolt.endY" :offset-x="controllerPos.x"
      :offset-y="controllerPos.y" />
    <div class="max-w-7xl mx-auto grid px-6 md:px-0 lg:grid-cols-2 gap-12 items-center w-full">
      <div class="space-y-8 z-10 order-2 lg:order-1">
        <div
          class="inline-flex items-center gap-2 px-4 py-2 rounded-full bg-(--electric-yellow/10) border border-(--electric-yellow/20) text-(--electric-yellow) font-medium text-sm">
          <Zap :size="16" fill="currentColor" />
          <span>Next-Gen Gaming Has Arrived</span>
        </div>

        <div class="space-y-4">
          <h1 class="text-5xl md:text-7xl font-black tracking-tighter leading-none text-white">
            DOMINATE
            <span
              style="filter: drop-shadow(0 0 8px rgba(255, 215, 0, 0.8)) drop-shadow(0 0 12px rgba(255, 215, 0, 0.5)) drop-shadow(0 2px 4px rgba(0, 0, 0, 0.3))"
              class="block text-transparent bg-clip-text bg-linear-to-r from-(--electric-yellow) to-(--electric-orange)">
              EVERY GAME
            </span>
          </h1>
          <p class="text-xl text-gray-400 max-w-xl leading-relaxed">
            Experience unparalleled precision and control with the Elite Thunder. Engineered for champions, designed for
            victory.
          </p>
          <div class="flex flex-wrap gap-4">
            <button
              class="bg-linear-to-b from-(--electric-yellow) to-(--electric-orange) text-xl  text-(--deep-black) px-12 py-3 rounded-lg font-semibold">
              Get Started
            </button>
            <button
              class="bg-transparent border-2 border-white  text-xl text-white px-12 py-3 hover:bg-white hover:text-(--deep-black) font-semibold rounded-lg transition-all">
              Explore Features
            </button>
          </div>
        </div>
      </div>
      <div class="relative order-1 lg:order-2">
        <div class="relative" ref="controllerContainer">
          <img src="../../assets/controller.png"
            class="animate-float animate-thunderPulse z-20 relative w-full h-auto max-w-xl object-contain transform hover:scale-105 transition-transform duration-500"
            style="filter: drop-shadow(0 0 20px rgba(251, 191, 36, 0.4)) drop-shadow(0 0 40px rgba(251, 191, 36, 0.2))">
        </div>
      </div>
    </div>
  </section>
</template>
<style scoped>
@keyframes pulse-glow {

  0%,
  100% {
    opacity: 0.4;
  }

  50% {
    opacity: 1;
  }
}

@keyframes thunderPulse {
  0%, 100% {
    filter: drop-shadow(0 0 5px rgba(255, 215, 0, 0.6)) 
            drop-shadow(0 0 8px rgba(255, 215, 0, 0.4));
    transform: translateY(0px) rotate(0deg) scale(1);
  }

  50% {
    filter: 
            drop-shadow(0 0 10px #FFD700) 
            drop-shadow(0 0 10px #FFD700);
    transform: translateY(-15px) rotate(-4deg) scale(1.05);
    
  }
}

@keyframes float {

  0%,
  100% {
    transform: translateY(0px) rotate(0deg);
  }

  50% {
    transform: translateY(-15px) rotate(-4deg);
  }
}

@keyframes energy-pulse {

  0%,
  100% {
    box-shadow: 0 0 20px rgba(251, 191, 36, 0.3),
      0 0 40px rgba(251, 191, 36, 0.2);
  }

  50% {
    box-shadow: 0 0 40px rgba(251, 191, 36, 0.6),
      0 0 80px rgba(251, 191, 36, 0.4);
  }
}

.animate-pulse-glow {
  animation: pulse-glow 2s ease-in-out infinite;
}

.animate-float {
  animation: float 4s ease-in-out infinite;
}

.animate-thunderPulse {
  animation: thunderPulse 3s ease-in-out infinite
}

.animate-energy-pulse {
  animation: energy-pulse 2s ease-in-out infinite;
}
</style>
