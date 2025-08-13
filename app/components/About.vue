<template>
    <div class="max-w-md mx-auto bg-gray-50 mb-[5rem]">
        <!-- Header Section -->
        <div class="bg-blue-500  py-2 flex items-center">
            <button @click="goBack" class="text-white mr-2 hover:bg-gray-500 rounded-full p-2">
                <svg class="w-6 h-6" fill="none" stroke="currentColor" viewBox="0 0 24 24">
                    <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7"></path>
                </svg>
            </button>
            <h1 class="text-white text-xl font-bold flex text-center pl-8">About us</h1>
        </div>

        <!-- Content Section -->
        <div class="px-6 py-6 bg-white">
            <div class="space-y-6 text-gray-900 leading-relaxed">
                <!-- Paragraph 1 -->
                <p class="text-base">
                    We are a full-service, universal loan application platform. We provide easy lending services with
                    low interest rates and a straightforward process. We have served many customers and are highly
                    recommended. We make it easy to obtain documents and complete loan requirements without collateral
                    for freelancers. We cooperate with banks through local subsidiaries, offering various loan types
                    including banking, private, leasing, finance personal, and loan insurance with low interest rates
                    for long periods.
                </p>

                <!-- Paragraph 2 -->
                <p class="text-base">
                    Our strengths lie in our value-added products and successful customer relationships. Our branches
                    maintain high standards for service and easy loans. We boast a large distribution network with over
                    1,500 operating branches and offices, providing loans to more than 1 million people nationwide, and
                    we have 16 offices spread across the country.
                </p>

                <!-- Paragraph 3 -->
                <p class="text-base">
                    We offer the best app solutions to make loans easier, faster, and more secure for our clients.
                </p>

                <!-- Paragraph 4 -->
                <p class="text-base">
                    Through selective acquisitions and organic growth, we are strategically positioned for increased
                    balance sheet strength and market expansion. As of 30 September 2022, we intend to become the
                    country's largest loan provider locally, leveraging consolidated resources, customer loans, assets
                    under management, capital, and our nationwide branch and loan network.
                </p>
            </div>
        </div>
    </div>
</template>

<script setup>
const goBack = () => {
    // Handle back navigation
    if (process.client) {
        window.history.back()
    }
}
</script>

<style scoped>
/* Additional custom styles if needed */
</style>
