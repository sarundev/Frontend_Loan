<template>
    <div class="min-h-screen bg-gray-50">
        <!-- Show Loan Application Form when showLoanForm is true -->
        <LoanApplicationForm v-if="showLoanForm && !showKYC && !showPersonalVerification" @close="showLoanForm = false"
            @loan-confirmed="handleLoanConfirmed" />

        <!-- Show KYC Identification when showKYC is true -->
        <KYCIdentification v-if="showKYC" :loan-data="currentLoanData" @back="handleKYCBack"
            @kyc-complete="handleKYCComplete" />

        <!-- Show Personal Verification when showPersonalVerification is true -->
        <PersonalVerification v-if="showPersonalVerification" @back="handlePersonalVerificationBack"
            @continue="handlePersonalVerificationComplete" />

        <!-- Show Main Content when all forms are false -->
        <div v-else-if="!showLoanForm && !showKYC && !showPersonalVerification" class="relative pb-20">
            <!-- Header Component -->
            <AppHeader :greeting="userGreeting" />

            <!-- Main Content Container -->
            <div class="max-w-md mx-auto px-4 py-4">
                <!-- Hero Banner Component -->
                <div class="mb-4">
                    <HeroBanner @apply="handleApply" />
                </div>

                <!-- Apply Button -->
                <div class="mb-6">
                    <ButtomApply @click="handleApply" />
                </div>

                <!-- Exchange Rates Component -->
                <div class="mb-6">
                    <ExchangeRates />
                </div>

                <!-- Inspiration Banner -->
                <!-- <div class="mb-6">
                    <InspirationBanner />
                </div> -->

                <!-- Loan Info Cards -->
                <div class="mb-6">
                    <LoanInfo />
                </div>
            </div>

        </div>
    </div>
</template>

<script setup>
import AppHeader from "~/components/AppHeader.vue";
import HeroBanner from "~/components/HeroBanner.vue";
import ExchangeRates from "~/components/ExchangeRates.vue";
import LoanInfo from "~/components/LoanInfo.vue";
import InspirationBanner from "~/components/InspirationBanner.vue";
import LoanApplicationForm from "~/components/LoanApplicationForm.vue";
import KYCIdentification from "~/components/KYCIdentification.vue";
import PersonalVerification from "~/components/PersonalVerification.vue";

// Reactive data
const userGreeting = ref("Hello, 097798338");
const showLoanForm = ref(false);
const showKYC = ref(false);
const showPersonalVerification = ref(false);
const currentLoanData = ref(null);

// Methods
const handleApply = () => {
    console.log("Apply button clicked");
    showLoanForm.value = true;
};

const handleLoanConfirmed = (data) => {
    console.log("Loan confirmed, showing KYC with data:", data);
    currentLoanData.value = data;
    showKYC.value = true;
    showLoanForm.value = false;
};

const handleKYCBack = () => {
    console.log("KYC back button clicked, hiding KYC");
    showKYC.value = false;
};

const handleKYCComplete = (kycData) => {
    console.log("KYC completed:", kycData);
    showKYC.value = false;
    showLoanForm.value = false;
    currentLoanData.value = null;
    showPersonalVerification.value = true;
};

const handlePersonalVerificationBack = () => {
    console.log("Personal Verification back button clicked, hiding personal verification");
    showPersonalVerification.value = false;
};

const handlePersonalVerificationComplete = () => {
    console.log("Personal verification completed");
    showPersonalVerification.value = false;
    // Reset all states
    showLoanForm.value = false;
    showKYC.value = false;
    currentLoanData.value = null;
};
</script>
