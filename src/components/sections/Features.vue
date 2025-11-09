<script setup lang="ts">
import { BatteryCharging, Gamepad2, Globe, Settings, Shield, Zap } from 'lucide-vue-next';
import ThunderContainer from '../ThunderContainer.vue';


const featureList = [
    {
        icon: Gamepad2,
        title: "Precision Control",
        description: "Hall-effect sensors and adjustable trigger stops provide unmatched accuracy and response times for competitive gaming."
    },
    {
        icon: Zap,
        title: "Lightning Fast",
        description: "1ms response time via low-latency wireless connection ensures your inputs register instantly for split-second victories."
    },
    {
        icon: BatteryCharging,
        title: "Extended Battery",
        description: "Play for days without charging. Our advanced battery technology delivers 50+ hours of continuous gameplay."
    },
    {
        icon: Settings,
        title: "Fully Customizable",
        description: "Remap buttons, adjust sensitivity curves, and create custom profiles for every game in your library."
    },
    {
        icon: Shield,
        title: "Premium Build",
        description: "Military-grade materials and precision engineering ensure your controller withstands years of intense gaming sessions."
    },
    {
        icon: Globe,
        title: "Cross-Platform",
        description: "Seamlessly switch between Xbox, PlayStation, PC, and mobile devices with a single button press."
    }
];

</script>

<template>
    <section class="bg-(--dark-gray)">
        <div class="max-w-7xl mx-auto px-4 py-16 space-y-16">
            <div class="text-center space-y-4">
                <h1 class="text-5xl text-white font-bold">You Are <span
                        class="text-(--electric-yellow) font-black uppercase tracking-tight">Winner</span></h1>
                <p className="text-gray-400 max-w-2xl mx-auto text-lg">
                    Every component of the Elite Thunder is designed to give you the competitive edge you need to win.
                </p>
            </div>

            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-8">
                <ThunderContainer :key="feature.title" v-for="feature in featureList" :icon="feature.icon"
                    :title="feature.title" :description="feature.description" />
            </div>
        </div>
    </section>
</template>