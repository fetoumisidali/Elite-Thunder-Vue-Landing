<script setup lang="ts">
import { Menu } from 'lucide-vue-next';
import NavLink from './NavLink.vue';
import { onMounted, onUnmounted, ref } from 'vue';


const isScrolled = ref(false)

const handleScroll = () => {
    isScrolled.value = window.scrollY > 50;
};

onMounted(() => {
    window.addEventListener('scroll', handleScroll);
})
onUnmounted(() => {
    window.removeEventListener('scroll', handleScroll);
})

</script>

<template>
    <header class="fixed top-0 left-0 z-50 right-0 px-4" :class="{ 'bg-black/70 backdrop-blur-md ' : isScrolled}">
        <div class="max-w-7xl mx-auto h-16 flex items-center justify-between">
            <div class="flex items-center">
                <img src="/controller-vector-no-bg.png" class="h-16 w-auto" alt="Logo">
                <h1 class="text-xl md:text-2xl font-bold text-white uppercase tracking-tighter">Elite <span
                    class="text-(--electric-yellow)">Thunder</span></h1>
            </div>
            <nav class="hidden md:flex items-center gap-6">
                <NavLink title="Features" />
                <NavLink title="Specs" />
                <a href=""
                    class="px-6 py-2 bg-(--electric-yellow/10) text-(--electric-yellow) border border-(--electric-yellow/50) rounded-full hover:bg-(--electric-yellow) hover:text-(--deep-black) transition-all duration-300 font-bold text-sm uppercase tracking-wider">
                    Pre-Order
                </a>
            </nav>
            <button @click="" class="md:hidden text-(--electric-yellow)">
                <Menu :size="24" />
            </button>
        </div>
    </header>
</template>
