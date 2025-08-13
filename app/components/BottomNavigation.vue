<template>
    <nav class="fixed bottom-0 left-0 right-0 z-[9999] bg-white border-t border-gray-200 shadow-lg">
        <!-- Mobile Layout -->
        <div class="flex justify-around items-center px-2 py-3 max-w-md mx-auto">
            <div v-for="(item, index) in navItems" :key="index"
                class="relative group cursor-pointer transition-all duration-200 min-h-[44px] min-w-[44px] flex items-center justify-center"
                :class="{ 'scale-105': activeIndex === index }" @click="setActiveItem(index)" role="button" tabindex="0"
                @keydown.enter="setActiveItem(index)" @keydown.space.prevent="setActiveItem(index)">

                <!-- Content container -->
                <div class="relative flex flex-col items-center justify-center px-2 py-1 rounded-lg transition-all duration-200"
                    :class="activeIndex === index ? 'bg-blue-50' : 'hover:bg-gray-50'">

                    <!-- Icon container -->
                    <div class="relative w-6 h-6 flex items-center justify-center mb-1">
                        <svg class="w-5 h-5 transition-all duration-200" :class="activeIndex === index
                            ? 'text-blue-600'
                            : 'text-blue-500'" viewBox="0 0 24 24" fill="currentColor" aria-hidden="true">
                            <path :d="item.icon" />
                        </svg>
                    </div>

                    <!-- Label -->
                    <span class="text-xs font-semibold transition-all duration-200" :class="activeIndex === index
                        ? 'text-blue-600'
                        : 'text-blue-500'">
                        {{ item.label }}
                    </span>
                </div>
            </div>
        </div>
    </nav>
</template>

<script setup>
import { ref, watch } from 'vue'

const props = defineProps({
    navItems: {
        type: Array,
        default: () => [
            {
                label: 'HOME',
                icon: 'M10 20v-6h4v6h5v-8h3L12 3 2 12h3v8z',
                route: '/'
            },
            {
                label: 'WALLET',
                icon: 'M21 18v1c0 1.1-.9 2-2 2H5c-1.11 0-2-.9-2-2V5c0-1.1.89-2 2-2h14c1.1 0 2 .9 2 2v1h-9c-.55 0-1 .45-1 1v8c0 .55.45 1 1 1h9zm-9-2h10V8H12v8zm4-2.5c-.83 0-1.5-.67-1.5-1.5s.67-1.5 1.5-1.5 1.5.67 1.5 1.5-.67 1.5-1.5 1.5z',
                route: '/wallet'
            },
            {
                label: 'PROFILE',
                icon: 'M12 12c2.21 0 4-1.79 4-4s-1.79-4-4-4-4 1.79-4 4 1.79 4 4 4zm0 2c-2.67 0-8 1.34-8 4v2h16v-2c0-2.66-5.33-4-8-4z',
                route: '/profile'
            }
        ]
    },
    activeIndex: {
        type: Number,
        default: 0
    }
})

const emit = defineEmits(['nav-change'])

const activeIndex = ref(props.activeIndex)

// Watch for prop changes to sync the internal state
watch(() => props.activeIndex, (newIndex) => {
    activeIndex.value = newIndex
})

const setActiveItem = (index) => {
    console.log('BottomNavigation: setActiveItem called with index:', index)
    if (activeIndex.value !== index) {
        activeIndex.value = index
        console.log('BottomNavigation: emitting nav-change event with index:', index)
        emit('nav-change', index)

        // Add haptic feedback for mobile devices
        if (navigator.vibrate) {
            navigator.vibrate(50)
        }
    } else {
        console.log('BottomNavigation: index is already active, not emitting event')
    }
}
</script>