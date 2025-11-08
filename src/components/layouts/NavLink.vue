<template>
    <a href=""
        class="text-gray-300 hover:text-(--electric-yellow) transition-colors text-sm font-semibold uppercase tracking-wider">{{ title }}</a>
</template>

<script setup lang="ts"> 
    defineProps<{title:string}>()
</script>