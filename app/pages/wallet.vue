<template>
    <div class="max-w-md mx-auto px-4 bg-blue-700 ">
        <div class="px-4 py-4 ">
            <h1 class="text-2xl font-bold text-white text-center">Wallet</h1>
        </div>
    </div>
    <div class="max-w-md mx-auto px-4 mb-[5rem]">
        <!-- Header -->


        <!-- Main Content -->
        <div class="max-w-md mx-auto px-6 py-8 space-y-6">
            <!-- Balance Section -->
            <div class="bg-gray-100 rounded-2xl shadow-lg p-6 border border-gray-200">
                <div class="space-y-4">
                    <div class="flex justify-between items-center">
                        <span class="text-gray-600 font-medium text-sm">Account Balance :</span>
                        <div class="bg-gray-300 text-gray-800 px-4 py-2 rounded-full text-sm font-semibold">
                            $0.00
                        </div>
                    </div>
                    <div class="flex justify-between items-center">
                        <span class="text-gray-600 font-medium text-sm">Withdraw Balance :</span>
                        <div
                            class="border-2 border-red-500 text-red-500 px-4 py-2 rounded-full text-sm font-semibold bg-transparent">
                            $undefined
                        </div>
                    </div>
                </div>
            </div>

            <!-- Loan Details Link -->
            <div
                class="flex items-center justify-center space-x-2 p-4 bg-white rounded-xl shadow-sm border border-gray-100 cursor-pointer hover:shadow-md transition-all duration-300 group">
                <svg class="w-5 h-5 text-blue-600 group-hover:scale-110 transition-transform duration-300"
                    viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path
                        d="M12 4.5C7 4.5 2.73 7.61 1 12c1.73 4.39 6 7.5 11 7.5s9.27-3.11 11-7.5c-1.73-4.39-6-7.5-11-7.5zM12 17c-2.76 0-5-2.24-5-5s2.24-5 5-5 5 2.24 5 5-2.24 5-5 5zm0-8c-1.66 0-3 1.34-3 3s1.34 3 3 3 3-1.34 3-3-1.34-3-3-3z"
                        fill="currentColor" />
                </svg>
                <span class="text-blue-600 font-semibold text-sm">LOAN DETAIL</span>
            </div>

            <!-- Action Buttons -->
            <div class="space-y-3">
                <button
                    class="w-full bg-gradient-to-r from-gray-400 to-gray-500 text-white font-semibold py-4 px-6 rounded-xl shadow-lg hover:shadow-xl transform hover:-translate-y-1 transition-all duration-300 uppercase tracking-wide">
                    Withdraw Money
                </button>
                <button
                    class="w-full bg-blue-500 text-white font-semibold py-4 px-6 rounded-xl shadow-lg hover:shadow-xl transform hover:-translate-y-1 transition-all duration-300 uppercase tracking-wide">
                    Loan Application
                </button>
            </div>

            <!-- Bank Icons Grid -->
            <div class="bg-white rounded-2xl shadow-lg p-6 border border-gray-100">
                <h3 class="text-lg font-semibold text-gray-800 mb-4 text-center">Supported Banks</h3>
                <div class="grid grid-cols-5 gap-4">
                    <div v-for="(bank, index) in banks" :key="index"
                        class="aspect-square rounded-2xl cursor-pointer transform hover:scale-110 transition-all duration-300 shadow-lg hover:shadow-xl overflow-hidden bg-white">
                        <NuxtImg :src="bank.image" :alt="bank.name" class="w-full h-full object-cover rounded-2xl"
                            sizes="sm:120px md:150px lg:200px" loading="lazy" />
                    </div>
                </div>
            </div>
        </div>
    </div>

</template>

<script setup>

// Bank data matching the exact image 100%
const banks = ref([
    {
        name: 'BPI',
        class: 'bpi',
        image: 'https://admin-api.online/storage/bank-list/bank-list-1715248699.jpg?w=120&h=120&fit=crop&auto=format&dpr=2',
        imageLarge: 'https://admin-api.online/storage/bank-list/bank-list-1715248699.jpg?w=200&h=200&fit=crop&auto=format&dpr=2',
    },
    {
        name: 'BDO Unibank',
        class: 'bdo',
        image: 'https://admin-api.online/storage/bank-list/bank-list-1715248711.png?w=120&h=120&fit=crop&auto=format&dpr=2',
        imageLarge: 'https://admin-api.online/storage/bank-list/bank-list-1715248711.png?w=200&h=200&fit=crop&auto=format&dpr=2',
    },
    {
        name: 'EastWest',
        class: 'ec',
        image: 'https://admin-api.online/storage/bank-list/bank-list-1715248800.jpg?w=120&h=120&fit=crop&auto=format&dpr=2',
        imageLarge: 'https://admin-api.online/storage/bank-list/bank-list-1715248800.jpg?w=200&h=200&fit=crop&auto=format&dpr=2',
    },
    {
        name: 'DBP',
        class: 'envelope',
        image: 'https://admin-api.online/storage/bank-list/bank-list-1715248893.jpg?w=120&h=120&fit=crop&auto=format&dpr=2',
        imageLarge: 'https://admin-api.online/storage/bank-list/bank-list-1715248893.jpg?w=200&h=200&fit=crop&auto=format&dpr=2',
    },
    {
        name: 'DBP',
        class: 'dbp',
        image: 'https://admin-api.online/storage/bank-list/bank-list-1715248928.png?w=120&h=120&fit=crop&auto=format&dpr=2',
        imageLarge: 'https://admin-api.online/storage/bank-list/bank-list-1715248928.png?w=200&h=200&fit=crop&auto=format&dpr=2',
    },
    {
        name: 'PNB',
        class: 'pnb',
        image: 'https://admin-api.online/storage/bank-list/bank-list-1715248972.png?w=120&h=120&fit=crop&auto=format&dpr=2',
        imageLarge: 'https://admin-api.online/storage/bank-list/bank-list-1715248972.png?w=200&h=200&fit=crop&auto=format&dpr=2',
    },
    {
        name: 'LANDBANKPay',
        class: 'landbank',
        image: 'https://admin-api.online/storage/bank-list/bank-list-1715249016.jpg?w=120&h=120&fit=crop&auto=format&dpr=2',
        imageLarge: 'https://admin-api.online/storage/bank-list/bank-list-1715249016.jpg?w=200&h=200&fit=crop&auto=format&dpr=2',
    },
    {
        name: 'PSBank',
        class: 'psbank',
        image: 'https://admin-api.online/storage/bank-list/bank-list-1715249049.png?w=120&h=120&fit=crop&auto=format&dpr=2',
        imageLarge: 'https://admin-api.online/storage/bank-list/bank-list-1715249049.png?w=200&h=200&fit=crop&auto=format&dpr=2',
    },
    {
        name: 'RCBC',
        class: 'rcbc',
        image: 'https://admin-api.online/storage/bank-list/bank-list-1715249125.png?w=120&h=120&fit=crop&auto=format&dpr=2',
        imageLarge: 'https://admin-api.online/storage/bank-list/bank-list-1715249125.png?w=200&h=200&fit=crop&auto=format&dpr=2',
    },
    {
        name: 'maya',
        class: 'maya',
        image: 'https://admin-api.online/storage/bank-list/bank-list-1715201523.png?w=120&h=120&fit=crop&auto=format&dpr=2',
        imageLarge: 'https://admin-api.online/storage/bank-list/bank-list-1715201523.png?w=200&h=200&fit=crop&auto=format&dpr=2',
    },
    {
        name: 'SECURITY BANK',
        class: 'security',
        image: 'https://admin-api.online/storage/bank-list/bank-list-1715249174.png?w=120&h=120&fit=crop&auto=format&dpr=2',
        imageLarge: 'https://admin-api.online/storage/bank-list/bank-list-1715249174.png?w=200&h=200&fit=crop&auto=format&dpr=2',
    },
    {
        name: 'UnionBank',
        class: 'unionbank',
        image: 'https://admin-api.online/storage/bank-list/bank-list-1715249225.jpg?w=120&h=120&fit=crop&auto=format&dpr=2',
        imageLarge: 'https://admin-api.online/storage/bank-list/bank-list-1715249225.jpg?w=200&h=200&fit=crop&auto=format&dpr=2',
    },
    {
        name: 'R BANK',
        class: 'rbank',
        image: 'https://admin-api.online/storage/bank-list/bank-list-1717093274.png?w=120&h=120&fit=crop&auto=format&dpr=2',
        imageLarge: 'https://admin-api.online/storage/bank-list/bank-list-1717093274.png?w=200&h=200&fit=crop&auto=format&dpr=2',
    },
    {
        name: 'GCash',
        class: 'gcash',
        image: 'https://admin-api.online/storage/bank-list/bank-list-1715201460.png?w=120&h=120&fit=crop&auto=format&dpr=2',
        imageLarge: 'https://admin-api.online/storage/bank-list/bank-list-1715201460.png?w=200&h=200&fit=crop&auto=format&dpr=2',
    },
    {
        name: 'CIMB BANK PHILIPPINES',
        class: 'cimb',
        image: 'https://admin-api.online/storage/bank-list/bank-list-1715201081.jpg?w=120&h=120&fit=crop&auto=format&dpr=2',
        imageLarge: 'https://admin-api.online/storage/bank-list/bank-list-1715201081.jpg?w=200&h=200&fit=crop&auto=format&dpr=2',
    },
])

const handleNavChange = (index) => {
    console.log('Navigation changed to index:', index)
    if (index === 0) {
        // Navigate to home page
        navigateTo('/')
    } else if (index === 2) {
        // Navigate to profile page
        navigateTo('/profile')
    }
}

// Utility function to generate different image sizes
const generateImageUrl = (baseUrl, width, height) => {
    const url = new URL(baseUrl)
    url.searchParams.set('w', width)
    url.searchParams.set('h', height)
    url.searchParams.set('fit', 'crop')
    url.searchParams.set('auto', 'format')
    url.searchParams.set('dpr', '2')
    return url.toString()
}

// Generate different image sizes for each bank
const getImageSizes = (bank) => {
    const baseUrl = bank.image.split('?')[0] // Remove existing parameters
    return {
        small: generateImageUrl(baseUrl, 80, 80),
        medium: generateImageUrl(baseUrl, 120, 120),
        large: generateImageUrl(baseUrl, 200, 200),
        xlarge: generateImageUrl(baseUrl, 300, 300)
    }
}
</script>
