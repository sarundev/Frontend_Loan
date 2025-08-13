<template>
    <div class="max-w-md mx-auto px-4 bg-blue-500 px-4 py-4">
        <h1 class="text-white text-xl font-bold">Profile</h1>
    </div>
    <div class="max-w-md mx-auto mb-[5rem]">

        <!-- Main Content -->
        <div class="px-4 py-8">
            <!-- Profile Picture -->
            <div class="flex justify-center mb-8">
                <div class="w-32 h-32 rounded-lg border-2 border-purple-200 overflow-hidden">
                    <img :src="userProfile.profileImage" :alt="userProfile.name" class="w-full h-full object-cover" />
                </div>
            </div>

            <!-- User Info -->
            <div class="text-center mb-6">
                <h2 class="text-xl font-bold text-gray-800">{{ userProfile.name }}</h2>
                <p class="text-gray-600">{{ userProfile.email }}</p>
                <p class="text-sm text-gray-500">Member since {{ userProfile.joinDate }}</p>
            </div>

            <!-- Menu Items -->
            <div class="space-y-3">
                <div v-for="(item, index) in menuItems" :key="item.id" @click="handleMenuItemClick(item)" :class="[
                    'rounded-lg p-4 flex items-center justify-between cursor-pointer transition-colors',
                    item.bgColor,
                    item.hoverColor
                ]">
                    <div class="flex items-center space-x-3">
                        <svg class="w-6 h-6" :class="item.iconColor" fill="currentColor" viewBox="0 0 20 20">
                            <path :d="item.iconPath" />
                        </svg>
                        <span :class="['font-medium', item.textColor]">{{ item.title }}</span>
                    </div>
                    <svg class="w-5 h-5" :class="item.iconColor" fill="currentColor" viewBox="0 0 20 20">
                        <path fill-rule="evenodd"
                            d="M7.293 14.707a1 1 0 010-1.414L10.586 10 7.293 6.707a1 1 0 011.414-1.414l4 4a1 1 0 010 1.414l-4 4a1 1 0 01-1.414 0z"
                            clip-rule="evenodd" />
                    </svg>
                </div>
            </div>


        </div>

        <!-- Bottom Navigation -->
        <BottomNavigation :active-index="2" @nav-change="handleNavChange" />
    </div>
</template>

<script setup>
import { ref } from 'vue'
import BottomNavigation from '~/components/BottomNavigation.vue'

// Reactive user profile data
const userProfile = ref({
    name: 'John Doe',
    email: 'john.doe@example.com',
    profileImage: 'https://images.unsplash.com/photo-1514888286974-6c03e2ca1dba?w=128&h=128&fit=crop&crop=face',
    joinDate: 'January 2024'
})

// Dynamic menu items data
const menuItems = ref([
    {
        id: 1,
        title: 'PERSONAL INFORMATION',
        iconPath: 'M10 9a3 3 0 100-6 3 3 0 000 6zm-7 9a7 7 0 1114 0H3z',
        bgColor: 'bg-blue-500',
        hoverColor: 'hover:bg-purple-200',
        iconColor: 'text-white',
        textColor: 'text-white',
        action: 'personal-info'
    },
    {
        id: 2,
        title: 'BENEFICIARY INFORMATION',
        iconPath: 'M4 4a2 2 0 00-2 2v1h16V6a2 2 0 00-2-2H4zM18 9H2v5a2 2 0 002 2h12a2 2 0 002-2V9zM4 13a1 1 0 011-1h1a1 1 0 110 2H5a1 1 0 01-1-1zm5-1a1 1 0 100 2h1a1 1 0 100-2H9z',
        bgColor: 'bg-blue-500',
        hoverColor: 'hover:bg-purple-200',
        iconColor: 'text-white',
        textColor: 'text-white',
        action: 'beneficiary-info'
    },
    {
        id: 3,
        title: 'LOAN CONTRACT',
        iconPath: 'M4 4a2 2 0 012-2h4.586A2 2 0 0112 2.586L15.414 6A2 2 0 0116 7.414V16a2 2 0 01-2 2H6a2 2 0 01-2-2V4zm2 6a1 1 0 011-1h6a1 1 0 110 2H7a1 1 0 01-1-1zm1 3a1 1 0 100 2h6a1 1 0 100-2H7z',
        bgColor: 'bg-blue-500',
        hoverColor: 'hover:bg-purple-200',
        iconColor: 'text-white',
        textColor: 'text-white',
        action: 'loan-contract'
    },
    {
        id: 4,
        title: 'PAYMENT SCHEDULE',
        iconPath: 'M6 2a1 1 0 00-1 1v1H4a2 2 0 00-2 2v10a2 2 0 002 2h12a2 2 0 002-2V6a2 2 0 00-2-2h-1V3a1 1 0 10-2 0v1H7V3a1 1 0 00-1-1zm0 5a1 1 0 000 2h8a1 1 0 100-2H6z',
        bgColor: 'bg-blue-500',
        hoverColor: 'hover:bg-purple-200',
        iconColor: 'text-white',
        textColor: 'text-white',
        action: 'payment-schedule'
    },
    {
        id: 5,
        title: 'TRANSACTIONS',
        iconPath: 'M4 2a1 1 0 011 1v2.101a7.002 7.002 0 0111.601 2.566 1 1 0 11-1.885.666A5.002 5.002 0 005.999 7H9a1 1 0 010 2H4a1 1 0 01-1-1V3a1 1 0 011-1zm.008 9.057a1 1 0 011.276.61A5.002 5.002 0 0014.001 13H11a1 1 0 110-2h5a1 1 0 011 1v5a1 1 0 11-2 0v-2.101a7.002 7.002 0 01-11.601-2.566 1 1 0 01.61-1.276z',
        bgColor: 'bg-blue-500',
        hoverColor: 'hover:bg-purple-200',
        iconColor: 'text-white',
        textColor: 'text-white',
        action: 'transactions'
    },
    {
        id: 6,
        title: 'ABOUT US',
        iconPath: 'M18 10c0 3.866-3.582 7-8 7a8.841 8.841 0 01-4.083-.98L2 17l1.338-3.123C2.493 12.767 2 11.434 2 10c0-3.866 3.582-7 8-7s8 3.134 8 7zM7 9H5v2h2V9zm8 0h-2v2h2V9zM9 9h2v2H9V9z',
        bgColor: 'bg-blue-500',
        hoverColor: 'hover:bg-purple-200',
        iconColor: 'text-white',
        textColor: 'text-white',
        action: 'about-us'
    },
    {
        id: 7,
        title: 'LOGOUT',
        iconPath: 'M3 3a1 1 0 00-1 1v12a1 1 0 102 0V4a1 1 0 00-1-1zm10.293 9.293a1 1 0 001.414 1.414l3-3a1 1 0 000-1.414l-3-3a1 1 0 10-1.414 1.414L14.586 9H7a1 1 0 100 2h7.586l-1.293 1.293z',
        bgColor: 'bg-blue-500',
        hoverColor: 'hover:bg-gray-50',
        iconColor: 'text-white',
        textColor: 'text-white',
        action: 'logout'
    }
])



// Handle menu item clicks
const handleMenuItemClick = (item) => {
    console.log('Menu item clicked:', item.title)

    switch (item.action) {
        case 'personal-info':

            navigateTo('/personal-information')
            break
        case 'beneficiary-info':
            navigateTo('/benificiary')
            break
        case 'loan-contract':
            navigateTo('/loancontract')
            break
        case 'payment-schedule':
            navigateTo('/payment')
            break
        case 'transactions':
            navigateTo('/transaction')
            break
        case 'about-us':
            navigateTo('/about')
            break
        case 'logout':
            // Handle logout
            console.log('Logging out...')
            // Add your logout logic here
            break
        default:
            console.log('Unknown action:', item.action)
    }
}

const handleNavChange = (index) => {
    console.log('Navigation changed to index:', index)
    if (index === 0) {
        // Navigate to home page
        navigateTo('/')
    } else if (index === 1) {
        // Navigate to wallet page
        navigateTo('/wallet')
    }
}
</script>
