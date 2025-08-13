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
                <h1 class="text-lg font-semibold text-white ml-4">Personal Verify</h1>
            </div>
        </div>

        <!-- Main Content -->
        <div class="px-4 py-6">
            <h2 class="text-xl font-bold text-gray-900 mb-6">Personal Information</h2>

            <div class="space-y-4">
                <!-- Actual Name -->
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">Actual Name</label>
                    <input v-model="formData.actualName" type="text"
                        class="w-full px-4 py-3 border border-red-500 rounded-lg bg-white focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-transparent"
                        :class="{ 'border-red-500': !formData.actualName }" />
                    <p class="text-xs text-red-600 mt-1">Required</p>
                </div>

                <!-- Identification Card No. -->
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">Identification Card No.</label>
                    <input v-model="formData.idNumber" type="text"
                        class="w-full px-4 py-3 border border-red-500 rounded-lg bg-white focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-transparent"
                        :class="{ 'border-red-500': !formData.idNumber }" />
                    <p class="text-xs text-red-600 mt-1">Required</p>
                </div>

                <!-- Gender -->
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">Gender</label>
                    <div class="relative">
                        <select v-model="formData.gender"
                            class="w-full px-4 py-3 border border-red-500 rounded-lg bg-white focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-transparent appearance-none"
                            :class="{ 'border-red-500': !formData.gender }">
                            <option value="">Select Gender</option>
                            <option value="male">Male</option>
                            <option value="female">Female</option>
                            <option value="other">Other</option>
                        </select>
                        <div class="absolute inset-y-0 right-0 flex items-center pr-3 pointer-events-none">
                            <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                                stroke-width="2" class="text-gray-400">
                                <polyline points="6,9 12,15 18,9" />
                            </svg>
                        </div>
                    </div>
                    <p class="text-xs text-red-600 mt-1">Required</p>
                </div>

                <!-- Current Job -->
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">Current Job</label>
                    <input v-model="formData.currentJob" type="text"
                        class="w-full px-4 py-3 border border-red-500 rounded-lg bg-white focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-transparent"
                        :class="{ 'border-red-500': !formData.currentJob }" />
                    <p class="text-xs text-red-600 mt-1">Required</p>
                </div>

                <!-- Stable Income -->
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">Stable Income</label>
                    <input v-model="formData.stableIncome" type="text"
                        class="w-full px-4 py-3 border border-red-500 rounded-lg bg-white focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-transparent"
                        :class="{ 'border-red-500': !formData.stableIncome }" />
                    <p class="text-xs text-red-600 mt-1">Required</p>
                </div>

                <!-- Loan Purpose -->
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">Loan Purpose</label>
                    <input v-model="formData.loanPurpose" type="text"
                        class="w-full px-4 py-3 border border-red-500 rounded-lg bg-white focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-transparent"
                        :class="{ 'border-red-500': !formData.loanPurpose }" />
                    <p class="text-xs text-red-600 mt-1">Required</p>
                </div>

                <!-- Current Address -->
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">Current Address</label>
                    <input v-model="formData.currentAddress" type="text"
                        class="w-full px-4 py-3 border border-red-500 rounded-lg bg-white focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-transparent"
                        :class="{ 'border-red-500': !formData.currentAddress }" />
                    <p class="text-xs text-red-600 mt-1">Required</p>
                </div>

                <!-- Name of Guarantor -->
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">Name of Guarantor</label>
                    <input v-model="formData.guarantorName" type="text"
                        class="w-full px-4 py-3 border border-red-500 rounded-lg bg-white focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-transparent"
                        :class="{ 'border-red-500': !formData.guarantorName }" />
                    <p class="text-xs text-red-600 mt-1">Required</p>
                </div>

                <!-- Phone number of Guarantor -->
                <div>
                    <label class="block text-sm font-medium text-gray-700 mb-1">Phone number of Guarantor</label>
                    <input v-model="formData.guarantorPhone" type="tel"
                        class="w-full px-4 py-3 border border-red-500 rounded-lg bg-white focus:outline-none focus:ring-2 focus:ring-red-500 focus:border-transparent"
                        :class="{ 'border-red-500': !formData.guarantorPhone }" />
                    <p class="text-xs text-red-600 mt-1">Required</p>
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

const emit = defineEmits(['back', 'continue'])

const formData = ref({
    actualName: '',
    idNumber: '',
    gender: '',
    currentJob: '',
    stableIncome: '',
    loanPurpose: '',
    currentAddress: '',
    guarantorName: '',
    guarantorPhone: ''
})

const isFormValid = computed(() => {
    return Object.values(formData.value).every(value => value.trim() !== '')
})

const handleContinue = () => {
    if (isFormValid.value) {
        console.log('Personal verification form submitted:', formData.value)

        // Store personal verification data in localStorage
        localStorage.setItem('personalVerificationData', JSON.stringify(formData.value))

        // Emit continue event with form data
        emit('continue', formData.value)

        // Parent component will handle navigation
    }
}
</script>
