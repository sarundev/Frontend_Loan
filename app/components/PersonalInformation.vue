<template>
    <div class="max-w-md mx-auto ">
        <!-- Header -->
        <div class="bg-blue-500 px-4 py-4">
            <div class="flex items-center justify-between">
                <button @click="goBack" class="p-2 rounded-lg hover:bg-blue-400 transition-colors duration-200">
                    <svg class="w-6 h-6 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
                    </svg>
                </button>
                <h1 class="text-lg font-bold text-white">Personal information</h1>
                <div class="w-10"></div>
            </div>
        </div>

        <!-- Profile Section -->
        <div class="px-4 py-6">
            <div class="bg-gray-100 rounded-2xl p-6 mb-6 text-center">
                <div class="mb-4">
                    <img src="https://images.unsplash.com/photo-1514888286974-6c03e2ca1dba?w=150&h=150&fit=crop&crop=face"
                        alt="Profile" class="w-24 h-24 rounded-2xl object-cover mx-auto" />
                </div>
                <div class="text-black font-semibold text-lg">097798338</div>
            </div>

            <!-- Personal Information Form -->
            <div class="bg-blue-600 rounded-t-3xl p-6">
                <h2 class="text-lg font-bold text-white text-center mb-6">Personal information</h2>

                <div class="space-y-4">
                    <!-- Actual Name -->
                    <div class="flex justify-between items-center py-3 border-b border-purple-500">
                        <label class="text-white font-medium">Actual Name</label>
                    </div>

                    <!-- Identification Card No -->
                    <div class="flex justify-between items-center py-3 border-b border-purple-500">
                        <label class="text-white font-medium">Identification Card No</label>
                        <div class="flex items-center space-x-2">
                            <span class="text-white tracking-widest">************</span>
                            <svg class="w-5 h-5 text-white" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                    d="M15 12a3 3 0 11-6 0 3 3 0 016 0z" />
                                <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                                    d="M2.458 12C3.732 7.943 7.523 5 12 5c4.478 0 8.268 2.943 9.542 7-1.274 4.057-5.064 7-9.542 7-4.477 0-8.268-2.943-9.542-7z" />
                            </svg>
                        </div>
                    </div>

                    <!-- Gender -->
                    <div class="flex justify-between items-center py-3 border-b border-purple-500">
                        <label class="text-white font-medium">Gender</label>
                    </div>

                    <!-- Current Job -->
                    <div class="flex justify-between items-center py-3 border-b border-purple-500">
                        <label class="text-white font-medium">Current job</label>
                    </div>

                    <!-- Stable Income -->
                    <div class="flex justify-between items-center py-3 border-b border-purple-500">
                        <label class="text-white font-medium">Stable income</label>
                    </div>

                    <!-- Loan Purpose -->
                    <div class="flex justify-between items-center py-3 border-b border-purple-500">
                        <label class="text-white font-medium">Loan purpose</label>
                    </div>

                    <!-- Current Address -->
                    <div class="flex justify-between items-center py-3 border-b border-purple-500">
                        <label class="text-white font-medium">Current address</label>
                    </div>

                    <!-- Name of Guarantor -->
                    <div class="flex justify-between items-center py-3 border-b border-purple-500">
                        <label class="text-white font-medium">Name of Guarantor</label>
                    </div>

                    <!-- Phone number of Guarantor -->
                    <div class="flex justify-between items-center py-3 border-b border-purple-500">
                        <label class="text-white font-medium">Phone number of Guarantor</label>
                    </div>

                    <!-- Borrowing Amount -->
                    <div class="flex justify-between items-center py-3 border-b border-purple-500">
                        <label class="text-white font-medium">Borrowing amount</label>
                        <span class="text-white">/ Months</span>
                    </div>

                    <!-- Monthly Payment -->
                    <div class="flex justify-between items-center py-3">
                        <label class="text-white font-medium">Monthly payment</label>
                    </div>
                </div>
            </div>
        </div>

        <!-- Bottom Navigation -->
        <div class="fixed bottom-0 left-0 right-0 bg-white border-t border-gray-200">
            <div class="flex justify-around py-3">
                <button class="flex flex-col items-center space-y-1">
                    <svg class="w-6 h-6 text-purple-600" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                            d="M3 12l2-2m0 0l7-7 7 7M5 10v10a1 1 0 001 1h3m10-11l2 2m-2-2v10a1 1 0 01-1 1h-3m-6 0a1 1 0 001-1v-4a1 1 0 011-1h2a1 1 0 011 1v4a1 1 0 001 1m-6 0h6" />
                    </svg>
                    <span class="text-xs font-semibold text-purple-600">HOME</span>
                </button>

                <button class="flex flex-col items-center space-y-1">
                    <svg class="w-6 h-6 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                            d="M3 10h18M7 15h1m4 0h1m-7 4h12a3 3 0 003-3V8a3 3 0 00-3-3H6a3 3 0 00-3 3v8a3 3 0 003 3z" />
                    </svg>
                    <span class="text-xs font-semibold text-gray-400">WALLET</span>
                </button>

                <button class="flex flex-col items-center space-y-1">
                    <svg class="w-6 h-6 text-gray-400" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2"
                            d="M16 7a4 4 0 11-8 0 4 4 0 018 0zM12 14a7 7 0 00-7 7h14a7 7 0 00-7-7z" />
                    </svg>
                    <span class="text-xs font-semibold text-gray-400">PROFILE</span>
                </button>
            </div>
        </div>

        <!-- Bottom Spacing for Navigation -->
        <div class="h-20"></div>
    </div>
</template>

<script setup>
// Component logic can be added here
const router = useRouter()

const goBack = () => {
    router.back()
}
</script>
