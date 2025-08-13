<template>
    <header class=" max-w-md mx-auto px-4 py-4">
        <div class="max-w-md mx-auto px-4 bg-blue-700">
            <div class="flex justify-between items-center py-4">
                <!-- User Greeting Section -->
                <div class="flex items-center">
                    <div>
                        <h1 class="text-white text-lg font-semibold">
                            {{ greeting }}
                        </h1>
                    </div>
                </div>

                <!-- Notification Icon -->
                <button @click="handleNotification"
                    class="relative p-2 text-white hover:bg-white/10 rounded-lg transition-all duration-200">
                    <svg class="w-6 h-6" viewBox="0 0 24 24" fill="none" stroke="currentColor">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                            d="M15 17h5l-5 5v-5zM10.5 3.75a6 6 0 0 1 6 6v3.75a2.25 2.25 0 0 0 4.5 0V9.75a8.25 8.25 0 0 0-16.5 0v3.75a2.25 2.25 0 0 0 4.5 0V9.75a6 6 0 0 1 6-6Z" />
                    </svg>
                </button>
            </div>
        </div>
    </header>
</template>

<script setup>
defineProps({
    greeting: {
        type: String,
        default: 'Hello, 097798338'
    }
})

const handleNotification = () => {
    // Handle notification click
    console.log('Notification clicked')
}
</script>
