<template>
    <div class="min-h-screen bg-gradient-to-br from-slate-50 via-blue-50 to-indigo-50">
        <!-- Show Verification Completed when showVerificationCompleted is true -->
        <VerificationCompleted v-if="showVerificationCompleted" @back="handleVerificationCompletedBack"
            @continue="handleVerificationCompletedContinue" />

        <!-- Show Bank Account Form when showBankForm is true -->
        <BankAccountForm v-else-if="showBankForm" @back="handleBankFormBack" @continue="handleBankFormComplete" />

        <!-- Show Final Confirmation when showFinalConfirmation is true -->
        <div v-else-if="showFinalConfirmation" class="min-h-screen bg-white">
            <!-- Header -->
            <div class="bg-gradient-to-r from-green-600 via-emerald-600 to-teal-600 px-6 py-6 shadow-lg">
                <div class="flex items-center max-w-md mx-auto">
                    <button @click="handleFinalConfirmationBack"
                        class="text-white p-3 hover:bg-white/20 rounded-xl transition-all duration-200 hover:scale-105 active:scale-95">
                        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                            stroke-width="2.5">
                            <path d="M15 18l-6-6 6-6" />
                        </svg>
                    </button>
                    <h1 class="text-xl font-bold text-white ml-4">Application Complete</h1>
                </div>
            </div>

            <!-- Main Content -->
            <div class="max-w-md mx-auto px-6 py-8">
                <!-- Success Status Card -->
                <div
                    class="bg-white rounded-2xl p-8 shadow-xl border border-gray-100 mb-8 transform hover:scale-[1.02] transition-all duration-300">
                    <div class="text-center">
                        <!-- Animated Success Icon -->
                        <div
                            class="relative w-20 h-20 bg-gradient-to-r from-green-400 to-emerald-500 rounded-full flex items-center justify-center mx-auto mb-6 shadow-lg">
                            <div
                                class="absolute inset-0 bg-gradient-to-r from-green-400 to-emerald-500 rounded-full animate-pulse opacity-75">
                            </div>
                            <svg width="36" height="36" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                                stroke-width="2.5" class="text-white relative z-10">
                                <path d="M22 11.08V12a10 10 0 1 1-5.93-9.14" />
                                <polyline points="22,4 12,14.01 9,11.01" />
                            </svg>
                        </div>

                        <h2 class="text-2xl font-bold text-gray-900 mb-3">Application Submitted!</h2>
                        <p class="text-gray-600 text-base leading-relaxed">Your loan application has been successfully
                            submitted. We will review your information and contact you soon.</p>

                        <!-- Status Badge -->
                        <div
                            class="inline-flex items-center px-4 py-2 bg-green-100 text-green-800 rounded-full text-sm font-medium mt-4">
                            <div class="w-2 h-2 bg-green-500 rounded-full mr-2 animate-pulse"></div>
                            Pending Review
                        </div>
                    </div>
                </div>

                <!-- Action Buttons -->
                <div class="space-y-4">
                    <button @click="goToHome"
                        class="w-full bg-blue-500 text-white font-semibold py-4 px-6 rounded-2xl shadow-lg hover:shadow-xl transform hover:scale-[1.02] active:scale-[0.98] transition-all duration-200 flex items-center justify-center space-x-3 group">
                        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                            stroke-width="2.5" class="group-hover:translate-x-1 transition-transform duration-200">
                            <path d="M3 9l9-7 9 7v11a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2z"></path>
                            <polyline points="9,22 9,12 15,12 15,22"></polyline>
                        </svg>
                        <span>Go to Home</span>
                    </button>
                </div>
            </div>
        </div>

        <!-- Show Original Identification Content when all forms are false -->
        <div v-else>
            <!-- Header -->
            <div class="bg-gradient-to-r from-indigo-600 via-purple-600 to-pink-600 px-6 py-6 shadow-lg">
                <div class="flex items-center max-w-md mx-auto">
                    <button @click="goBack"
                        class="text-white p-3 hover:bg-white/20 rounded-xl transition-all duration-200 hover:scale-105 active:scale-95">
                        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                            stroke-width="2.5">
                            <path d="M15 18l-6-6 6-6" />
                        </svg>
                    </button>
                    <h1 class="text-xl font-bold text-white ml-4">Verification Status</h1>
                </div>
            </div>

            <!-- Main Content -->
            <div class="max-w-md mx-auto px-6 py-8">
                <!-- Success Status Card -->
                <div v-if="kycData"
                    class="bg-white rounded-2xl p-8 shadow-xl border border-gray-100 mb-8 transform hover:scale-[1.02] transition-all duration-300">
                    <div class="text-center">
                        <!-- Animated Success Icon -->
                        <div
                            class="relative w-20 h-20 bg-gradient-to-r from-green-400 to-emerald-500 rounded-full flex items-center justify-center mx-auto mb-6 shadow-lg">
                            <div
                                class="absolute inset-0 bg-gradient-to-r from-green-400 to-emerald-500 rounded-full animate-pulse opacity-75">
                            </div>
                            <svg width="36" height="36" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                                stroke-width="2.5" class="text-white relative z-10">
                                <path d="M22 11.08V12a10 10 0 1 1-5.93-9.14" />
                                <polyline points="22,4 12,14.01 9,11.01" />
                            </svg>
                        </div>

                        <h2 class="text-2xl font-bold text-gray-900 mb-3">Verification Complete!</h2>
                        <p class="text-gray-600 text-base leading-relaxed">Your identity has been successfully verified
                            and
                            your account is now fully activated.</p>

                        <!-- Status Badge -->
                        <div
                            class="inline-flex items-center px-4 py-2 bg-green-100 text-green-800 rounded-full text-sm font-medium mt-4">
                            <div class="w-2 h-2 bg-green-500 rounded-full mr-2 animate-pulse"></div>
                            Verified
                        </div>
                    </div>
                </div>

                <!-- Uploaded Documents Card -->
                <div v-if="kycData?.photos" class="bg-white rounded-2xl p-6 shadow-xl border border-gray-100 mb-8">
                    <div class="flex items-center mb-6">
                        <div class="w-10 h-10 bg-blue-100 rounded-xl flex items-center justify-center mr-4">
                            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                                stroke-width="2" class="text-blue-600">
                                <path d="M14 2H6a2 2 0 0 0-2 2v16a2 2 0 0 0 2 2h12a2 2 0 0 0 2-2V8z"></path>
                                <polyline points="14,2 14,8 20,8"></polyline>
                                <line x1="16" y1="13" x2="8" y2="13"></line>
                                <line x1="16" y1="17" x2="8" y2="17"></line>
                                <polyline points="10,9 9,9 8,9"></polyline>
                            </svg>
                        </div>
                        <h3 class="text-lg font-semibold text-gray-900">Uploaded Documents</h3>
                    </div>

                    <div class="grid grid-cols-3 gap-4">
                        <div class="text-center group">
                            <div
                                class="relative w-20 h-20 mx-auto mb-3 rounded-xl overflow-hidden border-2 border-gray-200 group-hover:border-blue-300 transition-colors duration-200 shadow-sm">
                                <img v-if="kycData.photos.frontId" :src="kycData.photos.frontId" alt="Front ID"
                                    class="w-full h-full object-cover" />
                                <div v-else
                                    class="w-full h-full bg-gradient-to-br from-gray-50 to-gray-100 flex items-center justify-center">
                                    <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                                        stroke-width="2" class="text-gray-400">
                                        <rect x="3" y="3" width="18" height="18" rx="2" ry="2" />
                                        <circle cx="8.5" cy="8.5" r="1.5" />
                                        <polyline points="21,15 16,10 5,21" />
                                    </svg>
                                </div>
                                <!-- Success overlay -->
                                <div
                                    class="absolute inset-0 bg-green-500/20 flex items-center justify-center opacity-0 group-hover:opacity-100 transition-opacity duration-200">
                                    <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                                        stroke-width="2.5" class="text-white">
                                        <polyline points="20,6 9,17 4,12" />
                                    </svg>
                                </div>
                            </div>
                            <span class="text-xs font-medium text-gray-700">Front ID</span>
                        </div>

                        <div class="text-center group">
                            <div
                                class="relative w-20 h-20 mx-auto mb-3 rounded-xl overflow-hidden border-2 border-gray-200 group-hover:border-blue-300 transition-colors duration-200 shadow-sm">
                                <img v-if="kycData.photos.backId" :src="kycData.photos.backId" alt="Back ID"
                                    class="w-full h-full object-cover" />
                                <div v-else
                                    class="w-full h-full bg-gradient-to-br from-gray-50 to-gray-100 flex items-center justify-center">
                                    <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                                        stroke-width="2" class="text-gray-400">
                                        <rect x="3" y="3" width="18" height="18" rx="2" ry="2" />
                                        <circle cx="8.5" cy="8.5" r="1.5" />
                                        <polyline points="21,15 16,10 5,21" />
                                    </svg>
                                </div>
                                <!-- Success overlay -->
                                <div
                                    class="absolute inset-0 bg-green-500/20 flex items-center justify-center opacity-0 group-hover:opacity-100 transition-opacity duration-200">
                                    <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                                        stroke-width="2.5" class="text-white">
                                        <polyline points="20,6 9,17 4,12" />
                                    </svg>
                                </div>
                            </div>
                            <span class="text-xs font-medium text-gray-700">Back ID</span>
                        </div>

                        <div class="text-center group">
                            <div
                                class="relative w-20 h-20 mx-auto mb-3 rounded-xl overflow-hidden border-2 border-gray-200 group-hover:border-blue-300 transition-colors duration-200 shadow-sm">
                                <img v-if="kycData.photos.selfie" :src="kycData.photos.selfie" alt="Selfie"
                                    class="w-full h-full object-cover" />
                                <div v-else
                                    class="w-full h-full bg-gradient-to-br from-gray-50 to-gray-100 flex items-center justify-center">
                                    <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                                        stroke-width="2" class="text-gray-400">
                                        <rect x="3" y="3" width="18" height="18" rx="2" ry="2" />
                                        <circle cx="8.5" cy="8.5" r="1.5" />
                                        <polyline points="21,15 16,10 5,21" />
                                    </svg>
                                </div>
                                <!-- Success overlay -->
                                <div
                                    class="absolute inset-0 bg-green-500/20 flex items-center justify-center opacity-0 group-hover:opacity-100 transition-opacity duration-200">
                                    <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                                        stroke-width="2.5" class="text-white">
                                        <polyline points="20,6 9,17 4,12" />
                                    </svg>
                                </div>
                            </div>
                            <span class="text-xs font-medium text-gray-700">Selfie</span>
                        </div>
                    </div>
                </div>

                <!-- Loan Information Card -->
                <div v-if="loanData" class="bg-white rounded-2xl p-6 shadow-xl border border-gray-100 mb-8">
                    <div class="flex items-center mb-6">
                        <div class="w-10 h-10 bg-purple-100 rounded-xl flex items-center justify-center mr-4">
                            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                                stroke-width="2" class="text-purple-600">
                                <path d="M12 1v22M17 5H9.5a3.5 3.5 0 0 0 0 7h5a3.5 3.5 0 0 1 0 7H6"></path>
                            </svg>
                        </div>
                        <h3 class="text-lg font-semibold text-gray-900">Loan Application</h3>
                    </div>

                    <div class="space-y-4">
                        <div
                            class="flex justify-between items-center p-4 bg-gradient-to-r from-purple-50 to-pink-50 rounded-xl">
                            <div class="flex items-center">
                                <div class="w-8 h-8 bg-purple-100 rounded-lg flex items-center justify-center mr-3">
                                    <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                                        stroke-width="2" class="text-purple-600">
                                        <path d="M12 1v22M17 5H9.5a3.5 3.5 0 0 0 0 7h5a3.5 3.5 0 0 1 0 7H6"></path>
                                    </svg>
                                </div>
                                <span class="text-sm font-medium text-gray-700">Loan Amount</span>
                            </div>
                            <span class="text-lg font-bold text-gray-900">${{ loanData.amount?.toLocaleString()
                                }}</span>
                        </div>

                        <div
                            class="flex justify-between items-center p-4 bg-gradient-to-r from-blue-50 to-indigo-50 rounded-xl">
                            <div class="flex items-center">
                                <div class="w-8 h-8 bg-blue-100 rounded-lg flex items-center justify-center mr-3">
                                    <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                                        stroke-width="2" class="text-blue-600">
                                        <rect x="3" y="4" width="18" height="18" rx="2" ry="2"></rect>
                                        <line x1="16" y1="2" x2="16" y2="6"></line>
                                        <line x1="8" y1="2" x2="8" y2="6"></line>
                                        <line x1="3" y1="10" x2="21" y2="10"></line>
                                    </svg>
                                </div>
                                <span class="text-sm font-medium text-gray-700">Period</span>
                            </div>
                            <span class="text-lg font-bold text-gray-900">{{ loanData.period }} months</span>
                        </div>
                    </div>
                </div>

                <!-- Personal Verification Data Card -->
                <div v-if="personalVerificationData"
                    class="bg-white rounded-2xl p-6 shadow-xl border border-gray-100 mb-8">
                    <div class="flex items-center mb-6">
                        <div class="w-10 h-10 bg-green-100 rounded-xl flex items-center justify-center mr-4">
                            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                                stroke-width="2" class="text-green-600">
                                <path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"></path>
                                <circle cx="12" cy="7" r="4"></circle>
                            </svg>
                        </div>
                        <h3 class="text-lg font-semibold text-gray-900">Personal Information</h3>
                    </div>

                    <div class="grid grid-cols-1 md:grid-cols-2 gap-4">
                        <div class="p-4 bg-gradient-to-r from-green-50 to-emerald-50 rounded-xl">
                            <div class="flex items-center mb-2">
                                <div class="w-6 h-6 bg-green-100 rounded-lg flex items-center justify-center mr-2">
                                    <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                                        stroke-width="2" class="text-green-600">
                                        <path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2"></path>
                                        <circle cx="12" cy="7" r="4"></circle>
                                    </svg>
                                </div>
                                <span class="text-sm font-medium text-gray-700">Name</span>
                            </div>
                            <span class="text-lg font-bold text-gray-900">{{ personalVerificationData.actualName
                                }}</span>
                        </div>

                        <div class="p-4 bg-gradient-to-r from-blue-50 to-indigo-50 rounded-xl">
                            <div class="flex items-center mb-2">
                                <div class="w-6 h-6 bg-blue-100 rounded-lg flex items-center justify-center mr-2">
                                    <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                                        stroke-width="2" class="text-blue-600">
                                        <rect x="3" y="3" width="18" height="18" rx="2" ry="2" />
                                    </svg>
                                </div>
                                <span class="text-sm font-medium text-gray-700">ID Number</span>
                            </div>
                            <span class="text-lg font-bold text-gray-900">{{ personalVerificationData.idNumber }}</span>
                        </div>

                        <div class="p-4 bg-gradient-to-r from-purple-50 to-pink-50 rounded-xl">
                            <div class="flex items-center mb-2">
                                <div class="w-6 h-6 bg-purple-100 rounded-lg flex items-center justify-center mr-2">
                                    <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                                        stroke-width="2" class="text-purple-600">
                                        <path
                                            d="M16 4h2a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H6a2 2 0 0 1-2-2V6a2 2 0 0 1 2-2h2">
                                        </path>
                                        <rect x="8" y="2" width="8" height="4" rx="1" ry="1"></rect>
                                    </svg>
                                </div>
                                <span class="text-sm font-medium text-gray-700">Job</span>
                            </div>
                            <span class="text-lg font-bold text-gray-900">{{ personalVerificationData.currentJob
                                }}</span>
                        </div>

                        <div class="p-4 bg-gradient-to-r from-yellow-50 to-orange-50 rounded-xl">
                            <div class="flex items-center mb-2">
                                <div class="w-6 h-6 bg-yellow-100 rounded-lg flex items-center justify-center mr-2">
                                    <svg width="12" height="12" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                                        stroke-width="2" class="text-yellow-600">
                                        <path d="M12 1v22M17 5H9.5a3.5 3.5 0 0 0 0 7h5a3.5 3.5 0 0 1 0 7H6"></path>
                                    </svg>
                                </div>
                                <span class="text-sm font-medium text-gray-700">Income</span>
                            </div>
                            <span class="text-lg font-bold text-gray-900">{{ personalVerificationData.stableIncome
                                }}</span>
                        </div>
                    </div>
                </div>

                <!-- Action Buttons -->
                <div class="space-y-4">
                    <button @click="handleContinue"
                        class="w-full bg-blue-500 text-white font-semibold py-4 px-6 rounded-2xl shadow-lg hover:shadow-xl transform hover:scale-[1.02] active:scale-[0.98] transition-all duration-200 flex items-center justify-center space-x-3 group">
                        <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                            stroke-width="2.5" class="group-hover:translate-x-1 transition-transform duration-200">
                            <path d="M2.01 21 23 12 2.01 3 2 10l15 2-15 2z"></path>
                        </svg>
                        <span>Continue to Bank Account</span>
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import BankAccountForm from '~/components/BankAccountForm.vue'
import VerificationCompleted from '~/components/VerificationCompleted.vue'

// Reactive data
const kycData = ref(null)
const loanData = ref(null)
const personalVerificationData = ref(null)
const showVerificationCompleted = ref(false)
const showBankForm = ref(false)
const showFinalConfirmation = ref(false)

// Methods
const goBack = () => {
    navigateTo('/')
}

const goToProfile = () => {
    navigateTo('/profile')
}

const goToWallet = () => {
    navigateTo('/wallet')
}

const formatDate = (timestamp) => {
    if (!timestamp) return 'N/A'
    return new Date(timestamp).toLocaleDateString('en-US', {
        year: 'numeric',
        month: 'long',
        day: 'numeric',
        hour: '2-digit',
        minute: '2-digit'
    })
}

const handleContinue = () => {
    showBankForm.value = true
}

const handleVerificationCompletedBack = () => {
    showVerificationCompleted.value = false
    showBankForm.value = true
}

const handleVerificationCompletedContinue = () => {
    showVerificationCompleted.value = false
    showFinalConfirmation.value = true
}

const handleBankFormBack = () => {
    showBankForm.value = false
}

const handleBankFormComplete = () => {
    showBankForm.value = false
    showVerificationCompleted.value = true
}

const handleFinalConfirmationBack = () => {
    showFinalConfirmation.value = false
    showBankForm.value = true
}

const goToHome = () => {
    navigateTo('/')
}

onMounted(() => {
    // Get data from route query parameters or localStorage
    const route = useRoute()

    // Try to get data from route query
    if (route.query.kycData) {
        try {
            kycData.value = JSON.parse(decodeURIComponent(route.query.kycData))
        } catch (error) {
            console.error('Error parsing KYC data from route:', error)
        }
    }

    if (route.query.loanData) {
        try {
            loanData.value = JSON.parse(decodeURIComponent(route.query.loanData))
        } catch (error) {
            console.error('Error parsing loan data from route:', error)
        }
    }

    // Fallback to localStorage if route data is not available
    if (!kycData.value) {
        const storedKycData = localStorage.getItem('kycData')
        if (storedKycData) {
            try {
                kycData.value = JSON.parse(storedKycData)
            } catch (error) {
                console.error('Error parsing KYC data from localStorage:', error)
            }
        }
    }

    if (!loanData.value) {
        const storedLoanData = localStorage.getItem('loanData')
        if (storedLoanData) {
            try {
                loanData.value = JSON.parse(storedLoanData)
            } catch (error) {
                console.error('Error parsing loan data from localStorage:', error)
            }
        }
    }

    // Load personal verification data
    const storedPersonalVerificationData = localStorage.getItem('personalVerificationData')
    if (storedPersonalVerificationData) {
        try {
            personalVerificationData.value = JSON.parse(storedPersonalVerificationData)
        } catch (error) {
            console.error('Error parsing personal verification data from localStorage:', error)
        }
    }

    console.log('Identification page mounted with data:', {
        kycData: kycData.value,
        loanData: loanData.value,
        personalVerificationData: personalVerificationData.value
    })
})
</script>

<style scoped>
/* Custom scrollbar for webkit browsers */
::-webkit-scrollbar {
    width: 8px;
}

::-webkit-scrollbar-track {
    background: #f8fafc;
    border-radius: 4px;
}

::-webkit-scrollbar-thumb {
    background: linear-gradient(135deg, #6366f1, #8b5cf6, #ec4899);
    border-radius: 4px;
}

::-webkit-scrollbar-thumb:hover {
    background: linear-gradient(135deg, #4f46e5, #7c3aed, #db2777);
}

/* Smooth transitions for all interactive elements */
* {
    transition: all 0.3s cubic-bezier(0.4, 0, 0.2, 1);
}

/* Focus styles for accessibility */
button:focus {
    outline: 2px solid #6366f1;
    outline-offset: 2px;
}

/* Custom animations */
@keyframes float {

    0%,
    100% {
        transform: translateY(0px);
    }

    50% {
        transform: translateY(-10px);
    }
}

.animate-float {
    animation: float 3s ease-in-out infinite;
}

/* Glass morphism effect */
.glass {
    background: rgba(255, 255, 255, 0.25);
    backdrop-filter: blur(10px);
    border: 1px solid rgba(255, 255, 255, 0.18);
}

/* Enhanced shadows */
.shadow-glow {
    box-shadow: 0 0 20px rgba(99, 102, 241, 0.1);
}

.shadow-glow:hover {
    box-shadow: 0 0 30px rgba(99, 102, 241, 0.2);
}
</style>
