<template>
    <PaymentSchedule @back="handleBack" />
</template>

<script setup>
import PaymentSchedule from '../components/PaymentSchedule.vue';
const handleBack = () => {
    // Navigate back to the previous page using the router
    if (process.client) {
        window.history.back();
    }
}
</script>