<script setup lang="ts">
import { ref, onMounted } from 'vue'

const emit = defineEmits(['apply'])

const items = [
    '/images/pic.jpg',
    '/images/pic1.jpg',
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

const handleApply = () => {
    emit('apply')
}
</script>

<template>
    <div class="hero-banner">
        <!-- Carousel Section -->
        <div class="relative rounded-lg overflow-hidden mb-4">
            <UCarousel ref="carouselRef" v-slot="slotProps" :items="items" :ui="{ item: 'basis-full' }"
                class="rounded-lg overflow-hidden" indicators>
                <img v-if="slotProps?.item" :src="slotProps.item" class="w-full h-48 object-cover" draggable="false">
            </UCarousel>
        </div>
    </div>
</template>
