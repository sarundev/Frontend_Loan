<template>
    <div class="max-w-md mx-auto ">
        <!-- Header -->
        <div class="bg-blue-500 py-2">
            <div class="flex items-center">
                <button @click="goBack" class="text-white mr-4 p-2">
                    <div class="realtive hover:bg-gray-500 rounded-full p-2">

                        <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7">
                            </path>
                        </svg>
                    </div>
                </button>
                <h1 class="text-white font-bold text-xl flex justify-center items-center">Payment schedule</h1>
            </div>
        </div>

        <!-- Loan Information Section -->
        <div class="px-4 py-6">
            <div class="bg-blue-500 rounded-2xl p-6 mb-6">
                <h2 class="text-white font-bold text-xl mb-4">Loan information</h2>
                <div class="space-y-3">
                    <div class="text-white">Loan amount</div>
                    <div class="text-white">Loan term</div>
                    <div class="text-white">Interest rate</div>
                    <div class="text-white">Currency</div>
                </div>
            </div>

            <!-- Payment Details Section -->
            <div class="bg-white rounded-2xl border border-gray-200 overflow-hidden">
                <!-- Column Headers -->
                <div class="bg-blue-400 px-4 py-3">
                    <div class="grid grid-cols-6 gap-2 text-sm">
                        <div class="text-white font-bold text-center">No</div>
                        <div class="text-white font-bold text-center">Payment date</div>
                        <div class="text-white font-bold text-center">Principal payable</div>
                        <div class="text-white font-bold text-center">Interest payable</div>
                        <div class="text-white font-bold text-center bg-blue-500 px-2 py-1 rounded">Total Payable</div>
                        <div class="text-white font-bold text-center">Principal Balance</div>
                    </div>
                </div>

                <!-- Table Body -->
                <div class="max-h-64 overflow-y-auto">
                    <div v-for="(payment, index) in paymentSchedule" :key="index"
                        class="grid grid-cols-6 gap-2 px-4 py-3 text-sm border-b border-gray-100 hover:bg-gray-50">
                        <div class="text-center font-medium text-gray-700">{{ payment.no }}</div>
                        <div class="text-center text-gray-600">{{ payment.date }}</div>
                        <div class="text-center font-semibold text-green-600">${{ payment.principal }}</div>
                        <div class="text-center font-semibold text-yellow-600">${{ payment.interest }}</div>
                        <div class="text-center font-bold text-blue-600">${{ payment.totalPayable }}</div>
                        <div class="text-center font-semibold text-gray-700">${{ payment.principalBalance }}</div>
                    </div>
                </div>

                <!-- Scrollbar/Progress Indicator -->
                <div class="px-4 py-2">
                    <div class="bg-gray-300 h-2 rounded-full">
                        <div class="bg-gray-600 h-2 rounded-full w-1/3"></div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script setup>
// Define emits
const emit = defineEmits(['back'])

// Payment schedule data
const paymentSchedule = [
    { no: 1, date: '2024-01-15', principal: '833.33', interest: '70.83', totalPayable: '904.16', principalBalance: '9,166.67' },
    { no: 2, date: '2024-02-15', principal: '833.33', interest: '70.83', totalPayable: '904.16', principalBalance: '8,333.34' },
    { no: 3, date: '2024-03-15', principal: '833.33', interest: '70.83', totalPayable: '904.16', principalBalance: '7,500.01' },
    { no: 4, date: '2024-04-15', principal: '833.33', interest: '70.83', totalPayable: '904.16', principalBalance: '6,666.68' },
    { no: 5, date: '2024-05-15', principal: '833.33', interest: '70.83', totalPayable: '904.16', principalBalance: '5,833.35' },
    { no: 6, date: '2024-06-15', principal: '833.33', interest: '70.83', totalPayable: '904.16', principalBalance: '5,000.02' },
    { no: 7, date: '2024-07-15', principal: '833.33', interest: '70.83', totalPayable: '904.16', principalBalance: '4,166.69' },
    { no: 8, date: '2024-08-15', principal: '833.33', interest: '70.83', totalPayable: '904.16', principalBalance: '3,333.36' },
    { no: 9, date: '2024-09-15', principal: '833.33', interest: '70.83', totalPayable: '904.16', principalBalance: '2,500.03' },
    { no: 10, date: '2024-10-15', principal: '833.33', interest: '70.83', totalPayable: '904.16', principalBalance: '1,666.70' },
    { no: 11, date: '2024-11-15', principal: '833.33', interest: '70.83', totalPayable: '904.16', principalBalance: '833.37' },
    { no: 12, date: '2024-12-15', principal: '833.33', interest: '70.83', totalPayable: '904.16', principalBalance: '0.04' },
]

const goBack = () => {
    emit('back')
}
</script>

<style scoped>
/* Custom styles for the component */
</style>
