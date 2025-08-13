<template>
    <div class="max-w-md mx-auto bg-white">
        <!-- Header -->
        <div class="bg-blue-500 shadow-md">
            <div class=" py-2">
                <div class="flex items-center">
                    <button @click="goBack" class="p-2 rounded-full hover:bg-gray-500 transition-colors duration-200">
                        <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
                        </svg>
                    </button>
                    <h1 class="text-xl font-bold text-white mx-auto">Withdrawal History</h1>
                    <div class="w-10"></div> <!-- Spacer for centering -->
                </div>
            </div>
        </div>

        <!-- Main Content -->
        <div class="flex-1 flex flex-col items-center justify-center px-5 py-12">
            <!-- Receipt Icon -->
            <div class="mb-6">
                <svg width="120" height="120" viewBox="0 0 120 120" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <!-- Main receipt body -->
                    <path
                        d="M20 10C20 8.89543 20.8954 8 22 8H98C99.1046 8 100 8.89543 100 10V110C100 111.105 99.1046 112 98 112H22C20.8954 112 20 111.105 20 110V10Z"
                        fill="#F5F5F5" stroke="#E0E0E0" stroke-width="1" />

                    <!-- Jagged top edge -->
                    <path
                        d="M20 10L25 8L30 10L35 8L40 10L45 8L50 10L55 8L60 10L65 8L70 10L75 8L80 10L85 8L90 10L95 8L100 10"
                        stroke="#E0E0E0" stroke-width="1" fill="none" />

                    <!-- Horizontal lines representing text -->
                    <rect x="30" y="25" width="60" height="2" fill="#D0D0D0" rx="1" />
                    <rect x="30" y="35" width="45" height="2" fill="#D0D0D0" rx="1" />
                    <rect x="30" y="45" width="50" height="2" fill="#D0D0D0" rx="1" />
                    <rect x="30" y="55" width="40" height="2" fill="#D0D0D0" rx="1" />
                    <rect x="30" y="65" width="55" height="2" fill="#D0D0D0" rx="1" />
                    <rect x="30" y="75" width="35" height="2" fill="#D0D0D0" rx="1" />
                    <rect x="30" y="85" width="48" height="2" fill="#D0D0D0" rx="1" />

                    <!-- Grid pattern on the right side -->
                    <rect x="85" y="25" width="8" height="8" fill="#D0D0D0" rx="1" />
                    <rect x="85" y="40" width="8" height="8" fill="#D0D0D0" rx="1" />
                    <rect x="85" y="55" width="8" height="8" fill="#D0D0D0" rx="1" />
                    <rect x="85" y="70" width="8" height="8" fill="#D0D0D0" rx="1" />
                    <rect x="85" y="85" width="8" height="8" fill="#D0D0D0" rx="1" />
                </svg>
            </div>

            <!-- No history message -->
            <p class="text-lg font-bold text-black">No withdrawal history</p>
        </div>
    </div>
</template>

<script setup>
const goBack = () => {
    // Handle back navigation
    if (process.client) {
        window.history.back()
    }
}
</script>
