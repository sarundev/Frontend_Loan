<template>
    <div class="min-h-screen bg-white">
        <!-- Header -->
        <div class="bg-purple-600 px-4 py-4">
            <div class="flex items-center">
                <button @click="$emit('back')" class="text-white p-2">
                    <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                        <path d="M15 18l-6-6 6-6" />
                    </svg>
                </button>
                <h1 class="text-lg font-semibold text-white ml-4">Verification completed</h1>
            </div>
        </div>

        <!-- Main Content -->
        <div class="flex flex-col items-center justify-center px-4 py-12">
            <!-- Success Icon -->
            <div class="mb-6">
                <div class="w-20 h-20 bg-green-100 rounded-full flex items-center justify-center">
                    <svg width="40" height="40" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"
                        class="text-green-600">
                        <path d="M22 11.08V12a10 10 0 1 1-5.93-9.14" />
                        <polyline points="22,4 12,14.01 9,11.01" />
                    </svg>
                </div>
            </div>

            <!-- Success Message -->
            <div class="text-center mb-8">
                <h2 class="text-2xl font-bold text-gray-900 mb-2">Congratulations</h2>
                <p class="text-red-600 font-medium">Verification completed, please continue.</p>
            </div>

            <!-- Continue Button -->
            <div class="w-full max-w-sm">
                <button @click="handleContinue"
                    class="w-full flex items-center justify-center gap-2 px-6 py-4 bg-purple-600 text-white rounded-lg font-semibold hover:bg-purple-700 transition-colors duration-200">
                    <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                        <path d="M5 12h14M12 5l7 7-7 7" />
                    </svg>
                    CONTINUE
                </button>
            </div>
        </div>
    </div>
</template>

<script setup>
const handleContinue = () => {
    console.log('Verification completed, continuing...')
    // Emit continue event to parent component
    emit('continue')
}

defineEmits(['back', 'continue'])
</script>
