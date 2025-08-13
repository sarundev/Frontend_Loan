<template>
    <section class="bg-white rounded-lg p-4 shadow-md">
        <h2 class="text-xl font-bold text-gray-900 text-center mb-4">
            {{ title }}
        </h2>

        <!-- Exchange Rates Table -->
        <div class="space-y-3">
            <div v-for="rate in rates" :key="rate.currency"
                class="flex items-center justify-between p-3 bg-gray-50 rounded-lg hover:bg-gray-100 transition-colors duration-200">
                <!-- Currency Pair -->
                <div class="flex items-center gap-2">
                    <div class="flex items-center gap-1">
                        <span class="text-lg">{{ rate.fromFlag }}</span>
                        <span class="text-sm font-medium text-gray-800">{{ rate.fromCurrency }}</span>
                    </div>
                    <span class="text-gray-400">|</span>
                    <div class="flex items-center gap-1">
                        <span class="text-lg">{{ rate.toFlag }}</span>
                        <span class="text-sm font-medium text-gray-800">{{ rate.toCurrency }}</span>
                    </div>
                </div>

                <!-- Buy/Sell Rates -->
                <div class="flex gap-2">
                    <div
                        class="bg-purple-100 text-purple-700 px-3 py-1 rounded-lg text-center font-semibold text-sm min-w-[60px]">
                        {{ rate.buy }}
                    </div>
                    <div
                        class="bg-green-100 text-green-700 px-3 py-1 rounded-lg text-center font-semibold text-sm min-w-[60px]">
                        {{ rate.sell }}
                    </div>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
const props = defineProps({
    title: {
        type: String,
        default: 'Exchange Rates'
    },
    rates: {
        type: Array,
        default: () => [
            {
                currency: 'PHP | USD',
                fromCurrency: 'PHP',
                toCurrency: 'USD',
                fromFlag: '🇵🇭',
                toFlag: '🇺🇸',
                buy: '0.018',
                sell: '0.018'
            },
            {
                currency: 'PHP | EUR',
                fromCurrency: 'PHP',
                toCurrency: 'EUR',
                fromFlag: '🇵🇭',
                toFlag: '🇪🇺',
                buy: '0.016',
                sell: '0.016'
            },
            {
                currency: 'PHP | IDR',
                fromCurrency: 'PHP',
                toCurrency: 'IDR',
                fromFlag: '🇵🇭',
                toFlag: '🇮🇩',
                buy: '286.120',
                sell: '286.120'
            },
            {
                currency: 'PHP | MYR',
                fromCurrency: 'PHP',
                toCurrency: 'MYR',
                fromFlag: '🇵🇭',
                toFlag: '🇲🇾',
                buy: '0.075',
                sell: '0.075'
            },
            {
                currency: 'PHP | CNY',
                fromCurrency: 'PHP',
                toCurrency: 'CNY',
                fromFlag: '🇵🇭',
                toFlag: '🇨🇳',
                buy: '0.127',
                sell: '0.127'
            }
        ]
    }
})
</script>
