<template>
    <section class="space-y-3">
        <div v-for="(feature, index) in features" :key="index"
            class="bg-white rounded-lg p-4 shadow-md hover:shadow-lg transition-all duration-200 border border-gray-100">
            <div class="flex items-center justify-between gap-4">
                <div class="flex-1">
                    <h3 class="text-sm font-semibold text-gray-800 leading-relaxed">
                        {{ feature.text }}
                    </h3>
                </div>
                <div class="flex-shrink-0">
                    <div class="w-10 h-10 bg-blue-500 rounded-lg flex items-center justify-center">
                        <svg class="w-5 h-5 text-white" viewBox="0 0 24 24" fill="none">
                            <path :d="feature.icon" fill="currentColor" />
                        </svg>
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
const props = defineProps({
    features: {
        type: Array,
        default: () => [
            {
                text: 'APPLY NOW AND SIMPLE LOAN PROCESS',
                icon: 'M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-2 15l-5-5 1.41-1.41L10 14.17l7.59-7.59L19 8l-9 9z'
            },
            {
                text: 'LOAN LIMIT UP TO 2 MILLION PESO',
                icon: 'M9 12l2 2 4-4m6 2a9 9 0 11-18 0 9 9 0 0118 0z'
            },
            {
                text: 'NORMALLY THE APPLICATION GET APPROVE IN 24H AFTER MAKING APPLICATION SUCCESSFULLY',
                icon: 'M12 4V1L8 5l4 4V6c3.31 0 6 2.69 6 6 0 1.01-.25 1.97-.7 2.8l1.46 1.46C19.54 15.03 20 13.57 20 12c0-4.42-3.58-8-8-8zm0 14c-3.31 0-6-2.69-6-6 0-1.01.25-1.97.7-2.8L5.24 7.74C4.46 8.97 4 10.43 4 12c0 4.42 3.58 8 8 8v3l4-4-4-4v3z'
            }
        ]
    }
})
</script>
