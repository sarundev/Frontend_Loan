<template>
    <div v-if="isVisible" class="fixed inset-0 bg-black bg-opacity-50 z-50 flex items-center justify-center p-4">
        <div class="bg-white rounded-2xl w-full max-w-md max-h-[90vh] overflow-hidden shadow-2xl">
            <!-- Popup Header -->
            <div class="bg-blue-500 py-2 flex items-center justify-between">
                <h2 class="text-lg font-semibold text-white text-center flex-1 text-center uppercase">Loan Agreement
                </h2>
                <button @click="closePopup"
                    class="p-2 rounded-full hover:bg-gray-500 transition-colors duration-200 flex items-center justify-center">
                    <svg width="20" height="20" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path d="M18 6L6 18M6 6L18 18" stroke="white" stroke-width="2" stroke-linecap="round"
                            stroke-linejoin="round" />
                    </svg>
                </button>
            </div>

            <!-- Popup Content -->
            <div class="p-4 overflow-y-auto max-h-[calc(90vh-140px)]">
                <!-- Document Header -->
                <div class="text-center mb-6">
                    <p class="text-sm text-gray-600 mb-1">REPUBLIC OF THE PHILIPPINES</p>
                    <p class="text-sm text-gray-600 mb-4">SECURITIES AND EXCHANGE COMMISSION</p>
                    <h3 class="text-xl font-bold text-gray-900">LOAN AGREEMENT</h3>
                </div>

                <!-- Loan Details -->
                <div class="mb-6 space-y-3">
                    <div class="flex justify-between">
                        <span class="text-gray-700 font-medium">Party A (Lender):</span>
                        <span class="text-gray-900">Loan</span>
                    </div>
                    <div class="flex justify-between">
                        <span class="text-gray-700 font-medium">Party B (Borrower) Mr. / Mrs:</span>
                        <span class="text-gray-900">{{ beneficiaryName || 'Not specified' }}</span>
                    </div>
                    <div class="flex justify-between">
                        <span class="text-gray-700 font-medium">Loan Number:</span>
                        <span class="text-gray-900">#{{ Math.floor(Math.random() * 1000000) }}</span>
                    </div>
                    <div class="flex justify-between">
                        <span class="text-gray-700 font-medium">Identification Card No:</span>
                        <span class="text-gray-900">ID-{{ Math.floor(Math.random() * 100000) }}</span>
                    </div>
                    <div class="flex justify-between">
                        <span class="text-gray-700 font-medium">Sign day:</span>
                        <span class="text-gray-900">{{ new Date().toLocaleDateString() }}</span>
                    </div>
                    <div class="flex justify-between">
                        <span class="text-gray-700 font-medium">Loan amount:</span>
                        <span class="text-gray-900 font-semibold">{{ loanAmount || 'undefined' }}</span>
                    </div>
                    <div class="flex justify-between">
                        <span class="text-gray-700 font-medium">Borrowed time:</span>
                        <span class="text-gray-900">{{ loanTerm || 'undefined' }} months</span>
                    </div>
                    <div class="flex justify-between">
                        <span class="text-gray-700 font-medium">Loan interest rate:</span>
                        <span class="text-gray-900">undefined% every month</span>
                    </div>
                </div>

                <!-- User Service Agreement -->
                <div class="mb-6">
                    <h4 class="text-lg font-bold text-gray-900 text-center mb-4">User Service Agreement</h4>
                    <p class="text-sm text-gray-700 leading-relaxed">
                        "Installment Agreement", the Lender and the Borrower agree to and jointly abide by this
                        Agreement.
                        Adhering to the principles of equity, voluntary, honesty and reputation, there is no
                        consensus,
                        this small loan agreement is signed and ensures compliance and performance by the parties.
                    </p>
                </div>

                <!-- Articles Section -->
                <div class="space-y-6">
                    <!-- Article 1 -->
                    <div>
                        <h5 class="text-base font-bold text-gray-900 mb-2">Article 1: Loan Form</h5>
                        <p class="text-sm text-gray-700 leading-relaxed">
                            Use an unsecured ID card to request a loan.
                        </p>
                    </div>

                    <!-- Article 2 -->
                    <div>
                        <h5 class="text-base font-bold text-gray-900 mb-2">Article 2: Premium Interest Rate</h5>
                        <p class="text-sm text-gray-700 leading-relaxed">
                            Interest rates, fines, service charges or any fees.
                        </p>
                    </div>

                    <!-- Article 3 -->
                    <div>
                        <h5 class="text-base font-bold text-gray-900 mb-2">Article 3: Borrower Responsibilities</h5>
                        <div class="text-sm text-gray-700 leading-relaxed space-y-2">
                            <p>(1) Pay interest at the same time.</p>
                            <p>(2) To give capital on time.</p>
                            <p>(3) If it is not possible to borrow money from the account due to the borrower's
                                problem,
                                the borrower should cooperate with the lender to finalize the payment.</p>
                            <p>(4) Comply with all the terms of the contract.</p>
                        </div>
                    </div>

                    <!-- Article 4 -->
                    <div>
                        <h5 class="text-base font-bold text-gray-900 mb-2">Article 4: Loan Guarantee</h5>
                        <p class="text-sm text-gray-700 leading-relaxed">
                            (1) In case the borrower borrows online without using collateral, the lender is at risk
                            of
                            lending.
                            The borrower must have a loan guarantee to check the liquidity of the borrower's
                            personal loan
                            minimum repayment capacity and creditworthiness. The lender reserves the right to
                            require
                            additional collateral or guarantees as deemed necessary.
                        </p>
                    </div>

                    <!-- Article 5 -->
                    <div>
                        <h5 class="text-base font-bold text-gray-900 mb-2">Article 5: Default and Penalties</h5>
                        <p class="text-sm text-gray-700 leading-relaxed">
                            In the event of default, the borrower shall be liable for all costs of collection,
                            including but not limited to legal fees, court costs, and any other expenses incurred
                            by the lender in enforcing this agreement.
                        </p>
                    </div>

                    <!-- Article 6 -->
                    <div>
                        <h5 class="text-base font-bold text-gray-900 mb-2">Article 6: Governing Law</h5>
                        <p class="text-sm text-gray-700 leading-relaxed">
                            This agreement shall be governed by and construed in accordance with the laws of
                            the Republic of the Philippines. Any disputes arising from this agreement shall
                            be resolved through appropriate legal channels.
                        </p>
                    </div>
                </div>

                <!-- Signature Section -->
                <div class="mt-8 pt-6 border-t border-gray-200">
                    <div class="grid grid-cols-2 gap-6">
                        <div class="text-center">
                            <p class="text-sm font-medium text-gray-700 mb-2">Lender Signature</p>
                            <div
                                class="h-16 border-2 border-dashed border-gray-300 rounded-lg flex items-center justify-center">
                                <span class="text-xs text-gray-500">Digital Signature</span>
                            </div>
                        </div>
                        <div class="text-center">
                            <p class="text-sm font-medium text-gray-700 mb-2">Borrower Signature</p>
                            <div
                                class="h-16 border-2 border-dashed border-gray-300 rounded-lg flex items-center justify-center">
                                <span class="text-xs text-gray-500">Digital Signature</span>
                            </div>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Popup Footer with Accept Button -->
            <div class="bg-gray-50 px-4 py-4   border-t border-gray-200">
                <button @click="acceptContract"
                    class="w-full bg-blue-500 text-white font-semibold py-4 px-6 rounded-lg shadow-lg hover:bg-purple-700 transition-colors duration-200 uppercase tracking-wide">
                    ACCEPT
                </button>
            </div>
        </div>
    </div>
</template>

<script setup>
import { watch, onMounted } from 'vue'

// Props for contract data
const props = defineProps({
    isVisible: {
        type: Boolean,
        default: false
    },
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
const emit = defineEmits(['close', 'accept'])

// Debug on mount
onMounted(() => {
    console.log('LoanAgreementPopup component mounted')
    console.log('Initial props:', props)
})

// Watch for prop changes
watch(() => props.isVisible, (newValue) => {
    console.log('isVisible changed to:', newValue)
})

watch(() => props.loanAmount, (newValue) => {
    console.log('loanAmount changed to:', newValue)
})

// Methods
const closePopup = () => {
    console.log('closePopup clicked')
    emit('close')
}

const acceptContract = () => {
    console.log('acceptContract clicked')
    emit('accept')
}
</script>
