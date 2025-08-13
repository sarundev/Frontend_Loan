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
                <h1 class="text-lg font-semibold text-white ml-4">Bank Account</h1>
            </div>
        </div>

        <!-- Main Content -->
        <div class="px-4 py-6">
            <h2 class="text-xl font-bold text-gray-900 mb-6">Beneficiary Bank Information</h2>

            <div class="space-y-4">
                <!-- Beneficiary Bank -->
                <div>
                    <input v-model="formData.beneficiaryBank" type="text" placeholder="Beneficiary Bank"
                        class="w-full px-4 py-3 border border-gray-300 rounded-lg bg-white focus:outline-none focus:ring-2 focus:ring-purple-500 focus:border-transparent" />
                </div>

                <!-- Account Name -->
                <div>
                    <input v-model="formData.accountName" type="text" placeholder="Account name"
                        class="w-full px-4 py-3 border border-gray-300 rounded-lg bg-white focus:outline-none focus:ring-2 focus:ring-purple-500 focus:border-transparent" />
                </div>

                <!-- Account Number -->
                <div>
                    <input v-model="formData.accountNumber" type="text" placeholder="Account number"
                        class="w-full px-4 py-3 border border-gray-300 rounded-lg bg-white focus:outline-none focus:ring-2 focus:ring-purple-500 focus:border-transparent" />
                </div>
            </div>

            <!-- Continue Button -->
            <div class="mt-8">
                <button @click="handleContinue" :disabled="!isFormValid" :class="[
                    'w-full flex items-center justify-center gap-2 px-6 py-4 rounded-lg font-semibold text-white transition-all duration-200',
                    isFormValid
                        ? 'bg-purple-600 hover:bg-purple-700'
                        : 'bg-gray-300 cursor-not-allowed'
                ]">
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
import { ref, computed } from 'vue'

const formData = ref({
    beneficiaryBank: '',
    accountName: '',
    accountNumber: ''
})

const isFormValid = computed(() => {
    return formData.value.beneficiaryBank.trim() &&
        formData.value.accountName.trim() &&
        formData.value.accountNumber.trim()
})

const emit = defineEmits(['back', 'continue'])

const handleContinue = () => {
    if (isFormValid.value) {
        console.log('Bank account form submitted:', formData.value)

        // Store bank account data in localStorage
        localStorage.setItem('bankAccountData', JSON.stringify(formData.value))

        // Emit continue event with form data
        emit('continue', formData.value)
    }
}
</script>
