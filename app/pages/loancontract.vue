<template>
    <LoanContract @back="handleBack" />
</template>

<script setup>
import LoanContract from '../components/LoanContract.vue';

const handleBack = () => {
    // Navigate back to the previous page using the router
    if (process.client) {
        window.history.back();
    }
}
</script>