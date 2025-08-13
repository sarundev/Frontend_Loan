<template>
    <div class="flex justify-center items-center w-full">
        <button :class="buttonClasses" :disabled="disabled || loading" @click="handleClick" :type="type">
            <div class="flex items-center justify-center gap-3">
                <!-- Loading Spinner -->
                <div v-if="loading" class="flex items-center justify-center">
                    <svg class="animate-spin w-5 h-5 text-white" width="20" height="20" viewBox="0 0 24 24" fill="none">
                        <circle class="opacity-25" cx="12" cy="12" r="10" stroke="currentColor" stroke-width="4">
                        </circle>
                        <path class="opacity-75" fill="currentColor"
                            d="M4 12a8 8 0 018-8V0C5.373 0 0 5.373 0 12h4zm2 5.291A7.962 7.962 0 014 12H0c0 3.042 1.135 5.824 3 7.938l3-2.647z">
                        </path>
                    </svg>
                </div>

                <!-- Icon -->
                <div v-if="!loading" class="flex items-center justify-center">
                    <svg class="w-5 h-5 text-white" fill="currentColor" viewBox="0 0 24 24">
                        <path
                            d="M12 2C6.48 2 2 6.48 2 12s4.48 10 10 10 10-4.48 10-10S17.52 2 12 2zm-2 15l-5-5 1.41-1.41L10 14.17l7.59-7.59L19 8l-9 9z" />
                    </svg>
                </div>

                <!-- Text -->
                <span v-if="!loading" class="font-bold text-white">{{ text }}</span>
                <span v-else class="font-bold">{{ loadingText }}</span>
            </div>
        </button>
    </div>
</template>

<script setup lang="ts">
import { computed } from 'vue'

interface Props {
    text?: string
    variant?: 'primary' | 'secondary' | 'outline' | 'ghost' | 'danger' | 'blue'
    size?: 'sm' | 'md' | 'lg'
    disabled?: boolean
    loading?: boolean
    loadingText?: string
    icon?: any
    type?: 'button' | 'submit' | 'reset'
    fullWidth?: boolean
    rounded?: boolean
}

const props = withDefaults(defineProps<Props>(), {
    text: 'APPLY NOW',
    variant: 'primary',
    size: 'lg',
    disabled: false,
    loading: false,
    loadingText: 'Loading...',
    type: 'button',
    fullWidth: true,
    rounded: false
})

const emit = defineEmits<{
    click: [event: MouseEvent]
}>()

const handleClick = (event: MouseEvent) => {
    console.log('ButtomApply: handleClick called')
    console.log('ButtomApply: disabled =', props.disabled, 'loading =', props.loading)
    if (!props.disabled && !props.loading) {
        console.log('ButtomApply: emitting click event')
        emit('click', event)
    } else {
        console.log('ButtomApply: button is disabled or loading, not emitting event')
    }
}

const buttonClasses = computed(() => {
    const baseClasses = [
        'inline-flex items-center justify-center font-bold transition-all duration-200 ease-in-out focus:outline-none focus:ring-2 focus:ring-offset-2 disabled:opacity-50 disabled:cursor-not-allowed uppercase tracking-wide',
        props.fullWidth ? 'w-full' : '',
        props.rounded ? 'rounded-full' : 'rounded-lg'
    ]

    // Size classes
    const sizeClasses = {
        sm: 'px-3 py-1.5 text-sm',
        md: 'px-4 py-2 text-base',
        lg: 'px-6 py-3 text-lg'
    }

    // Variant classes
    const variantClasses = {
        primary: 'bg-blue-500',
        secondary: 'bg-gray-600 text-white hover:bg-gray-700 focus:ring-gray-500 shadow-sm hover:shadow-md',
        outline: 'border-2 border-purple-600 text-purple-600 hover:bg-purple-50 focus:ring-purple-500 bg-transparent',
        ghost: 'text-purple-600 hover:bg-purple-50 focus:ring-purple-500 bg-transparent',
        danger: 'bg-red-600 text-white hover:bg-red-700 focus:ring-red-500 shadow-sm hover:shadow-md',
        blue: 'bg-blue-500 text-white hover:bg-blue-600 focus:ring-blue-500 shadow-lg hover:shadow-xl transform hover:scale-105'
    }

    return [
        ...baseClasses,
        sizeClasses[props.size],
        variantClasses[props.variant]
    ].join(' ')
})
</script>
