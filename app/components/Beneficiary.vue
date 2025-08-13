<template>
    <div class="max-w-md mx-auto bg-white flex flex-col font-sans">
        <!-- Header -->
        <div class="bg-blue-500 py-4">
            <div class="flex items-center gap-4">
                <button @click="goBack" class="p-2 flex items-center justify-center">
                    <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path d="M15 18L9 12L15 6" stroke="white" stroke-width="2" stroke-linecap="round"
                            stroke-linejoin="round" />
                    </svg>
                </button>
                <h1 class="text-white text-lg font-bold flex-1">Beneficiary information</h1>
            </div>
        </div>

        <!-- Main Content -->
        <div class="flex-1 flex items-center justify-center p-5">
            <button
                class="bg-blue-500 text-white border-none rounded-2xl px-10 py-5 text-lg font-semibold cursor-pointer shadow-lg shadow-purple-500/30 transition-all duration-200 hover:-translate-y-0.5 hover:shadow-xl hover:shadow-purple-500/40 active:translate-y-0 min-w-[200px] text-center">
                Bank account
            </button>
        </div>


    </div>
</template>

<script setup>
const router = useRouter()

const goBack = () => {
    router.back()
}
</script>
