<template>
    <div class="max-w-md mx-auto bg-white min-h-screen">
        <!-- Header -->
        <div class="bg-blue-500 px-4 py-2">
            <div class="flex items-center space-x-3">
                <button @click="goBack"
                    class="p-2 rounded-full hover:bg-gray-500 transition-colors duration-200 flex items-center justify-center">
                    <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path d="M15 18L9 12L15 6" stroke="white" stroke-width="2" stroke-linecap="round"
                            stroke-linejoin="round" />
                    </svg>
                </button>
                <h1 class="text-lg font-semibold text-white uppercase">Loan contract</h1>
            </div>
        </div>

        <!-- Main Content -->
        <div class="px-4 py-6 space-y-6">
            <!-- Contract Information Card -->
            <div class="bg-blue-500 rounded-2xl p-2 shadow-lg">
                <h2 class="text-lg font-semibold text-white mb-6 text-center">Your contract information</h2>

                <div class="space-y-4">
                    <!-- Loan Amount -->
                    <div class="flex justify-between items-center py-2 border-b border-purple-500 last:border-b-0">
                        <span class="text-purple-100 font-medium">Loan amount</span>
                        <span class="text-white font-semibold">{{ loanAmount || 'undefined' }}</span>
                    </div>

                    <!-- Loan Term -->
                    <div class="flex justify-between items-center py-2 border-b border-purple-500 last:border-b-0">
                        <span class="text-purple-100 font-medium">Loan term</span>
                        <span class="text-white font-semibold">{{ loanTerm || '' }}</span>
                    </div>

                    <!-- Beneficiary Name -->
                    <div class="flex justify-between items-center py-2 border-b border-purple-500 last:border-b-0">
                        <span class="text-purple-100 font-medium">Beneficiary name</span>
                        <span class="text-white font-semibold">{{ beneficiaryName || '' }}</span>
                    </div>
                </div>
            </div>

            <!-- View Contract Button -->
            <div class="max-w-md mx-auto">
                <button @click="showContractPopup"
                    class="w-full bg-blue-500 text-white font-semibold py-4 px-6 rounded-lg shadow-md hover:bg-blue-600 transition-colors duration-200 uppercase tracking-wider">
                    VIEW CONTRACT
                </button>
            </div>
        </div>



        <!-- Loan Agreement Popup Component -->
        <LoanAgreementPopup :is-visible="showPopup" :loan-amount="loanAmount" :loan-term="loanTerm"
            :beneficiary-name="beneficiaryName" @close="closeContractPopup" @accept="acceptContract" />
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'
import LoanAgreementPopup from './LoanAgreementPopup.vue'

// Props for contract data
const props = defineProps({
    loanAmount: {
        type: [String, Number],
        default: null
    },
    loanTerm: {
        type: String,
        default: ''
    },
    beneficiaryName: {
        type: String,
        default: ''
    }
})

// Emits for events
const emit = defineEmits(['back', 'view-contract', 'accept-contract'])

// State for popup
const showPopup = ref(false)


// Methods
const goBack = () => {

    emit('back')
}

const showContractPopup = () => {
    console.log('showContractPopup clicked')
    showPopup.value = true
    console.log('showPopup value:', showPopup.value)
    emit('view-contract')
}

const closeContractPopup = () => {
    console.log('closeContractPopup called')
    showPopup.value = false
}

const acceptContract = () => {
    console.log('acceptContract called')
    showPopup.value = false
    emit('accept-contract')
}
</script>
