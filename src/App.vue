<script setup lang="ts">
import { onMounted } from 'vue';
import Navbar from './components/layouts/Navbar.vue';
import Hero from './components/sections/Hero.vue';
import { useEliteThunder } from './helpers/useThunderLog';
import Features from './components/sections/Features.vue';


  const { log } = useEliteThunder();

  onMounted(() =>{
    log()
  })

</script>

<template>
  <Navbar />
  <Hero />
  <Features />
</template>