<template>
    <div class="min-h-screen bg-gradient-to-br from-gray-50 to-gray-100 mb-[5rem]">
        <!-- Navigation Header -->
        <div class="bg-white border-b border-gray-200 px-4 sm:px-6 py-4 sticky top-0 z-10">
            <div class="flex items-center justify-between max-w-md mx-auto">
                <button @click="$emit('close')"
                    class="p-2 rounded-lg text-gray-600 hover:bg-gray-100 transition-colors duration-200">
                    <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                        <path d="M15 18l-6-6 6-6" />
                    </svg>
                </button>
                <h1 class="text-lg font-semibold text-gray-900">Choose a loan</h1>
                <div class="w-10"></div>
            </div>
        </div>

        <!-- Main Content Container -->
        <div class="max-w-md mx-auto px-4 sm:px-6 pb-8">
            <!-- Amount Section -->
            <div class="mt-6 bg-white rounded-2xl shadow-sm border border-gray-200 p-4 sm:p-6">
                <div class="flex items-center gap-3 mb-4 sm:mb-6">
                    <div
                        class="w-4 h-4 sm:w-6 sm:h-6 bg-gray-500 rounded-full flex items-center justify-center text-white font-semibold text-sm sm:text-lg">
                        ₱
                    </div>
                    <span class="text-sm sm:text-base font-medium text-gray-700">Enter the amount you need to
                        borrow</span>
                </div>

                <div class="flex flex-col sm:flex-row gap-3 mb-4">
                    <input v-model="loanAmount" type="number" placeholder="Enter the amount..."
                        class="flex-1 px-3 sm:px-4 py-3 sm:py-4 border border-gray-300 rounded-xl text-sm sm:text-base focus:outline-none focus:ring-2 focus:ring-purple-500 focus:border-transparent transition-all duration-200"
                        @input="calculateLoan" />
                    <div
                        class="flex items-center justify-center gap-2 px-3 sm:px-4 py-3 sm:py-4 border border-gray-300 rounded-xl bg-white cursor-pointer hover:border-purple-300 transition-colors duration-200 min-w-[120px] sm:min-w-[140px]">
                        <span class="text-xs sm:text-sm font-medium text-gray-700">Philippines</span>
                    </div>
                </div>

                <div class="flex justify-between text-xs sm:text-sm text-gray-500">
                    <span>From 70,000 ₱</span>
                    <span>Up to 3,000,000 ₱</span>
                </div>
            </div>

            <!-- Loan Period Section -->
            <div class="mt-4 bg-white rounded-2xl shadow-sm border border-gray-200 p-4 sm:p-6">
                <div class="flex items-center gap-3 mb-4 sm:mb-6">
                    <div
                        class="w-4 h-4 sm:w-6 sm:h-6 bg-gray-500 rounded-full flex items-center justify-center text-white">
                        <svg width="16" height="16" class="sm:w-5 sm:h-5" viewBox="0 0 24 24" fill="none"
                            stroke="currentColor" stroke-width="2">
                            <circle cx="12" cy="12" r="10" />
                            <polyline points="12,6 12,12 16,14" />
                        </svg>
                    </div>
                    <span class="text-sm sm:text-base font-medium text-gray-700">Loan period</span>
                </div>

                <div class="grid grid-cols-2 gap-2 sm:gap-3">
                    <button v-for="period in loanPeriods" :key="period.value" :class="[
                        'px-3 sm:px-4 py-3 sm:py-4 rounded-xl border text-xs sm:text-sm font-medium transition-all duration-200',
                        selectedPeriod === period.value
                            ? 'border-blue-600 bg-blue-500 text-white shadow-lg shadow-purple-200'
                            : 'border-gray-300 bg-white text-gray-700 hover:border-gray-500 hover:bg-blue-50'
                    ]" @click="selectPeriod(period.value)">
                        {{ period.label }}
                    </button>
                </div>
            </div>

            <!-- Loan Information Card -->
            <div class="mt-4 bg-white rounded-2xl shadow-lg border border-gray-200 p-4 sm:p-6">
                <h3 class="text-base sm:text-lg font-semibold text-gray-900 mb-4 sm:mb-6">Loan information</h3>

                <div class="space-y-3 sm:space-y-4">
                    <div class="flex justify-between items-center py-2 sm:py-3 border-b border-gray-100">
                        <span class="text-xs sm:text-sm text-gray-600">Amount of money</span>
                        <span class="text-xs sm:text-sm font-medium text-gray-900">{{ formatCurrency(loanAmount || 0)
                            }}</span>
                    </div>

                    <div class="flex justify-between items-center py-2 sm:py-3 border-b border-gray-100">
                        <span class="text-xs sm:text-sm text-gray-600">Monthly interest rate</span>
                        <span class="text-xs sm:text-sm font-medium text-gray-900">0.5%</span>
                    </div>

                    <div class="flex justify-between items-center py-2 sm:py-3 border-b border-gray-100">
                        <span class="text-xs sm:text-sm text-gray-600">Loan term</span>
                        <span class="text-xs sm:text-sm font-medium text-gray-900">{{ selectedPeriod || 0 }}
                            Months</span>
                    </div>

                    <div class="flex justify-between items-center py-2 sm:py-3 border-b border-gray-100">
                        <span class="text-xs sm:text-sm text-gray-600">Principal</span>
                        <span class="text-xs sm:text-sm font-medium text-gray-900">{{ formatCurrency(principal)
                            }}</span>
                    </div>

                    <div class="flex justify-between items-center py-2 sm:py-3 border-b border-gray-100">
                        <span class="text-xs sm:text-sm text-gray-600">Interest Amount</span>
                        <span class="text-xs sm:text-sm font-medium text-gray-900">{{ formatCurrency(interestAmount)
                            }}</span>
                    </div>

                    <div class="flex justify-between items-center py-2 sm:py-3 border-b border-gray-100">
                        <span class="text-xs sm:text-sm text-gray-600">Payment Amount</span>
                        <span class="text-sm sm:text-lg font-semibold text-gray-600">{{ formatCurrency(paymentAmount)
                            }}</span>
                    </div>

                    <div class="bg-red-50 border border-red-200 rounded-lg p-2 sm:p-3 text-center">
                        <span class="text-xs text-red-600 font-medium">*This is just an estimate</span>
                    </div>

                    <div class="flex justify-between items-center py-2 sm:py-3">
                        <span class="text-xs sm:text-sm text-gray-600">Disbursement date</span>
                        <span class="text-xs sm:text-sm font-medium text-gray-900">{{ disbursementDate }}</span>
                    </div>
                </div>
            </div>




            <!-- Confirmation Button -->
            <div class="mt-6">
                <button @click="confirmLoan" :class="[
                    'w-full flex items-center justify-center gap-2 px-4 sm:px-6 py-3 sm:py-4 rounded-2xl font-semibold text-sm sm:text-base transition-all duration-200',
                    canConfirm
                        ? 'bg-gradient-to-r from-purple-600 to-purple-700 text-white shadow-lg shadow-purple-200 hover:from-purple-700 hover:to-purple-800 transform hover:scale-[1.02]'
                        : 'bg-gray-300 text-gray-500 cursor-not-allowed'
                ]" :disabled="!canConfirm">
                    <span>LOAN CONFIRMATION</span>
                    <svg width="18" height="18" class="sm:w-5 sm:h-5" viewBox="0 0 24 24" fill="none"
                        stroke="currentColor" stroke-width="2">
                        <path d="M5 12h14M12 5l7 7-7 7" />
                    </svg>
                </button>
            </div>


        </div>
    </div>

    <!-- Confirmation Dialog -->
    <LoanConfirmationDialog :is-visible="showConfirmationDialog" :loan-amount="parseFloat(loanAmount) || 0"
        :loan-period="selectedPeriod" @cancel="handleLoanCancel" @agree="handleLoanAgreement" />
</template>

<script setup>
import { ref, computed, onMounted } from 'vue'
import LoanConfirmationDialog from './LoanConfirmationDialog.vue'

// Reactive data
const loanAmount = ref('')
const selectedPeriod = ref(12)
const agreedToTerms = ref(false)
const showConfirmationDialog = ref(false)

// Loan periods
const loanPeriods = [
    { label: '6 MONTHS', value: 6 },
    { label: '12 MONTHS', value: 12 },
    { label: '24 MONTHS', value: 24 },
    { label: '36 MONTHS', value: 36 }
]

// Computed properties
const principal = computed(() => {
    return parseFloat(loanAmount.value) || 0
})

const interestAmount = computed(() => {
    const amount = parseFloat(loanAmount.value) || 0
    const period = selectedPeriod.value || 12
    const monthlyRate = 0.005 // 0.5%
    return amount * monthlyRate * period
})

const paymentAmount = computed(() => {
    return principal.value + interestAmount.value
})

const canConfirm = computed(() => {
    return loanAmount.value && parseFloat(loanAmount.value) >= 70000
})

const disbursementDate = computed(() => {
    const date = new Date()
    date.setDate(date.getDate() + 30) // 30 days from now
    return date.toLocaleDateString('en-US', {
        month: 'long',
        day: 'numeric',
        year: 'numeric'
    })
})

// Methods
const selectPeriod = (period) => {
    selectedPeriod.value = period
    calculateLoan()
}

const calculateLoan = () => {
    // Trigger reactivity
    loanAmount.value = loanAmount.value
}

const formatCurrency = (amount) => {
    return new Intl.NumberFormat('en-PH', {
        style: 'currency',
        currency: 'PHP',
        minimumFractionDigits: 0,
        maximumFractionDigits: 0
    }).format(amount)
}

const confirmLoan = () => {
    if (canConfirm.value) {
        showConfirmationDialog.value = true
    }
}

const handleLoanAgreement = (data) => {
    console.log('Loan confirmed:', {
        amount: data.amount,
        period: data.period,
        paymentAmount: paymentAmount.value
    })
    showConfirmationDialog.value = false
    // Emit event to navigate to KYC identification
    console.log('Emitting loan-confirmed event...')
    emit('loan-confirmed', {
        amount: data.amount,
        period: data.period,
        paymentAmount: paymentAmount.value
    })
    console.log('Event emitted successfully')
}

const handleLoanCancel = () => {
    showConfirmationDialog.value = false
}

// Emits
const emit = defineEmits(['close', 'loan-confirmed'])

onMounted(() => {
    // Set default values
    selectedPeriod.value = 12
})
</script>
