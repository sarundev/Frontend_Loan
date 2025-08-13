<template>
    <div class="min-h-screen bg-gray-50">
        <!-- Header -->
        <div class="bg-white border-b border-gray-200 px-4 py-4">
            <h1 class="text-xl font-bold text-gray-900">Component Demo</h1>
            <p class="text-sm text-gray-600 mt-1">Showcasing all the new loan application components</p>
        </div>

        <!-- Component Navigation -->
        <div class="max-w-4xl mx-auto px-4 py-6">
            <div class="grid grid-cols-1 md:grid-cols-2 lg:grid-cols-3 gap-4">
                <!-- Bank Account Form -->
                <div class="bg-white rounded-lg shadow-sm border border-gray-200 p-4">
                    <h3 class="font-semibold text-gray-900 mb-2">Bank Account Form</h3>
                    <p class="text-sm text-gray-600 mb-4">Beneficiary bank information form</p>
                    <button @click="showComponent = 'bankAccount'"
                        class="w-full px-4 py-2 bg-purple-600 text-white rounded-lg hover:bg-purple-700 transition-colors">
                        View Component
                    </button>
                </div>

                <!-- KYC Identification -->
                <div class="bg-white rounded-lg shadow-sm border border-gray-200 p-4">
                    <h3 class="font-semibold text-gray-900 mb-2">KYC Identification</h3>
                    <p class="text-sm text-gray-600 mb-4">Photo upload for identity verification</p>
                    <button @click="showComponent = 'kyc'"
                        class="w-full px-4 py-2 bg-purple-600 text-white rounded-lg hover:bg-purple-700 transition-colors">
                        View Component
                    </button>
                </div>

                <!-- Personal Verification -->
                <div class="bg-white rounded-lg shadow-sm border border-gray-200 p-4">
                    <h3 class="font-semibold text-gray-900 mb-2">Personal Verification</h3>
                    <p class="text-sm text-gray-600 mb-4">Personal information form with validation</p>
                    <button @click="showComponent = 'personal'"
                        class="w-full px-4 py-2 bg-purple-600 text-white rounded-lg hover:bg-purple-700 transition-colors">
                        View Component
                    </button>
                </div>

                <!-- Loan Confirmation Dialog -->
                <div class="bg-white rounded-lg shadow-sm border border-gray-200 p-4">
                    <h3 class="font-semibold text-gray-900 mb-2">Loan Confirmation</h3>
                    <p class="text-sm text-gray-600 mb-4">Confirmation popup dialog</p>
                    <button @click="showComponent = 'confirmation'"
                        class="w-full px-4 py-2 bg-purple-600 text-white rounded-lg hover:bg-purple-700 transition-colors">
                        View Component
                    </button>
                </div>

                <!-- Verification Completed -->
                <div class="bg-white rounded-lg shadow-sm border border-gray-200 p-4">
                    <h3 class="font-semibold text-gray-900 mb-2">Verification Completed</h3>
                    <p class="text-sm text-gray-600 mb-4">Success screen after verification</p>
                    <button @click="showComponent = 'completed'"
                        class="w-full px-4 py-2 bg-purple-600 text-white rounded-lg hover:bg-purple-700 transition-colors">
                        View Component
                    </button>
                </div>

                <!-- Back to Demo -->
                <div class="bg-white rounded-lg shadow-sm border border-gray-200 p-4">
                    <h3 class="font-semibold text-gray-900 mb-2">Back to Demo</h3>
                    <p class="text-sm text-gray-600 mb-4">Return to component overview</p>
                    <button @click="showComponent = null"
                        class="w-full px-4 py-2 bg-gray-600 text-white rounded-lg hover:bg-gray-700 transition-colors">
                        Back to Overview
                    </button>
                </div>
            </div>
        </div>

        <!-- Component Display Area -->
        <div v-if="showComponent" class="fixed inset-0 bg-white z-50">
            <!-- Bank Account Form -->
            <BankAccountForm v-if="showComponent === 'bankAccount'" @back="showComponent = null" />

            <!-- KYC Identification -->
            <KYCIdentification v-if="showComponent === 'kyc'" @back="showComponent = null" />

            <!-- Personal Verification -->
            <PersonalVerification v-if="showComponent === 'personal'" @back="showComponent = null" />

            <!-- Verification Completed -->
            <VerificationCompleted v-if="showComponent === 'completed'" @back="showComponent = null" />

            <!-- Loan Confirmation Dialog (overlay) -->
            <div v-if="showComponent === 'confirmation'"
                class="min-h-screen bg-gray-900 flex items-center justify-center">
                <div class="bg-white rounded-lg p-6 max-w-md mx-4">
                    <h3 class="text-lg font-bold text-gray-900 mb-4">Loan Confirmation Dialog Demo</h3>
                    <p class="text-gray-600 mb-4">This component shows as a popup overlay. Click the button below to see
                        it in action.</p>
                    <div class="space-y-3">
                        <button @click="showConfirmationDialog = true"
                            class="w-full px-4 py-2 bg-purple-600 text-white rounded-lg hover:bg-purple-700 transition-colors">
                            Show Confirmation Dialog
                        </button>
                        <button @click="showComponent = null"
                            class="w-full px-4 py-2 bg-gray-600 text-white rounded-lg hover:bg-gray-700 transition-colors">
                            Back to Overview
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <!-- Confirmation Dialog -->
        <LoanConfirmationDialog :is-visible="showConfirmationDialog" :loan-amount="1000000" :loan-period="6"
            @cancel="showConfirmationDialog = false" @agree="handleLoanAgreement" />
    </div>
</template>

<script setup>
import { ref } from 'vue'
import BankAccountForm from '~/components/BankAccountForm.vue'
import KYCIdentification from '~/components/KYCIdentification.vue'
import PersonalVerification from '~/components/PersonalVerification.vue'
import LoanConfirmationDialog from '~/components/LoanConfirmationDialog.vue'
import VerificationCompleted from '~/components/VerificationCompleted.vue'

const showComponent = ref(null)
const showConfirmationDialog = ref(false)

const handleLoanAgreement = (data) => {
    console.log('Loan agreed:', data)
    showConfirmationDialog.value = false
    // You can navigate to the next step here
}
</script>
