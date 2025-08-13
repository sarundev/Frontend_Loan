<template>
    <div v-if="isVisible" class="fixed inset-0 bg-black bg-opacity-50 flex items-center justify-center z-50 p-4">
        <div class="bg-white rounded-lg max-w-sm w-full mx-4">
            <!-- Dialog Content -->
            <div class="p-6 text-center">
                <!-- Warning Icon -->
                <div class="flex justify-center mb-4">
                    <div class="w-16 h-16 bg-yellow-100 rounded-full flex items-center justify-center">
                        <svg width="32" height="32" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                            stroke-width="2" class="text-yellow-600">
                            <circle cx="12" cy="12" r="10" />
                            <line x1="12" y1="8" x2="12" y2="12" />
                            <line x1="12" y1="16" x2="12.01" y2="16" />
                        </svg>
                    </div>
                </div>

                <!-- Title -->
                <h3 class="text-lg font-bold text-gray-900 mb-3">Confirm</h3>

                <!-- Message -->
                <p class="text-gray-700 mb-6">
                    Agree to borrow {{ formatCurrency(loanAmount) }} term {{ loanPeriod }} months?
                </p>

                <!-- Action Buttons -->
                <div class="flex gap-3">
                    <button @click="handleCancel"
                        class="flex-1 px-4 py-3 bg-red-500 text-white rounded-lg font-semibold hover:bg-red-600 transition-colors duration-200">
                        CANCEL
                    </button>
                    <button @click="handleAgree"
                        class="flex-1 px-4 py-3 bg-purple-600 text-white rounded-lg font-semibold hover:bg-purple-700 transition-colors duration-200">
                        AGREE
                    </button>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
import { defineProps, defineEmits } from 'vue'

const props = defineProps({
    isVisible: {
        type: Boolean,
        default: false
    },
    loanAmount: {
        type: Number,
        default: 0
    },
    loanPeriod: {
        type: Number,
        default: 6
    }
})

const emit = defineEmits(['cancel', 'agree'])

const formatCurrency = (amount) => {
    return new Intl.NumberFormat('en-PH', {
        style: 'currency',
        currency: 'PHP',
        minimumFractionDigits: 0,
        maximumFractionDigits: 0
    }).format(amount)
}

const handleCancel = () => {
    emit('cancel')
}

const handleAgree = () => {
    emit('agree', {
        amount: props.loanAmount,
        period: props.loanPeriod
    })
}
</script>
