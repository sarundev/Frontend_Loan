<script setup lang="ts">
import { ref, onMounted } from 'vue'

const items = [
    'https://admin-api.online/storage/promotion/promotion-1731564812.jpg',

]

const carouselRef = ref()

onMounted(() => {
    setInterval(() => {
        if (!carouselRef.value) return

        if (carouselRef.value.page === carouselRef.value.pages) {
            return carouselRef.value.select(0)
        }

        carouselRef.value.next()
    }, 3000)
})
</script>

<template>
    <UCarousel ref="carouselRef" v-slot="slotProps" :items="items" :ui="{ item: 'basis-full' }"
        class="rounded-lg overflow-hidden" indicators>
        <img v-if="slotProps?.item" :src="slotProps.item" class="w-full h-64 object-cover" draggable="false">
    </UCarousel>
</template>
