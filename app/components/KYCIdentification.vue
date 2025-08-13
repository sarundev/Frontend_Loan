<template>
    <div class="min-h-screen bg-gray-50 mb-[5rem]">
        <!-- Header -->
        <div class="bg-purple-600 px-4 py-4 shadow-sm">
            <div class="flex items-center max-w-md mx-auto">
                <button @click="$emit('back')" class="text-white p-2 hover:bg-purple-700 rounded-lg transition-colors">
                    <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                        <path d="M15 18l-6-6 6-6" />
                    </svg>
                </button>
                <h1 class="text-lg font-semibold text-white ml-4">KYC Identification</h1>
            </div>
        </div>

        <!-- Main Content -->
        <div class="max-w-md mx-auto px-4 py-6">
            <h2 class="text-xl font-bold text-gray-900 text-center mb-2">Identity Verification</h2>
            <p class="text-gray-600 text-center mb-6 text-sm">Please upload clear photos of your identification
                documents</p>

            <!-- Status Message -->
            <div v-if="isKYCReady"
                class="flex items-center justify-center gap-2 mb-6 p-4 bg-green-50 border border-green-200 rounded-xl">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"
                    class="text-green-600 flex-shrink-0">
                    <path d="M22 11.08V12a10 10 0 1 1-5.93-9.14" />
                    <polyline points="22,4 12,14.01 9,11.01" />
                </svg>
                <span class="text-green-700 font-medium text-sm">All documents uploaded successfully</span>
            </div>

            <!-- Verification Success Message -->
            <div v-if="verificationSuccess"
                class="flex items-center justify-center gap-2 mb-6 p-4 bg-green-50 border border-green-200 rounded-xl animate-pulse">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"
                    class="text-green-600 flex-shrink-0">
                    <path d="M22 11.08V12a10 10 0 1 1-5.93-9.14" />
                    <polyline points="22,4 12,14.01 9,11.01" />
                </svg>
                <span class="text-green-700 font-medium text-sm">Verification successful! Redirecting...</span>
            </div>

            <!-- Verification Error Message -->
            <div v-if="verificationError"
                class="flex items-center justify-center gap-2 mb-6 p-4 bg-red-50 border border-red-200 rounded-xl">
                <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"
                    class="text-red-600 flex-shrink-0">
                    <circle cx="12" cy="12" r="10" />
                    <line x1="15" y1="9" x2="9" y2="15" />
                    <line x1="9" y1="9" x2="15" y2="15" />
                </svg>
                <span class="text-red-700 font-medium text-sm">{{ verificationError }}</span>
            </div>

            <!-- Progress Indicator -->
            <div class="mb-6">
                <div class="flex justify-between text-xs text-gray-500 mb-2">
                    <span>Progress</span>
                    <span>{{ uploadedCount }}/3 documents</span>
                </div>
                <div class="w-full bg-gray-200 rounded-full h-2">
                    <div class="bg-purple-600 h-2 rounded-full transition-all duration-300"
                        :style="{ width: `${(uploadedCount / 3) * 100}%` }"></div>
                </div>
            </div>

            <!-- Photo Upload Sections -->
            <div class="space-y-4">
                <!-- Front ID Card -->
                <div class="border border-gray-200 rounded-xl p-4 bg-white shadow-sm hover:shadow-md transition-shadow">
                    <div class="flex flex-col sm:flex-row sm:items-center gap-4">
                        <div class="relative flex-shrink-0">
                            <div class="w-20 h-20 sm:w-16 sm:h-16 bg-gray-50 rounded-xl flex items-center justify-center border-2 border-dashed border-gray-300 hover:border-purple-400 transition-colors cursor-pointer"
                                @click="openFileInput('frontId')" @dragover.prevent="handleDragOver"
                                @drop.prevent="handleDrop($event, 'frontId')" @dragenter.prevent="handleDragEnter"
                                @dragleave.prevent="handleDragLeave">

                                <!-- File Input (Hidden) -->
                                <input ref="frontIdInput" type="file" accept="image/*" class="hidden"
                                    @change="handleFileSelect($event, 'frontId')" />

                                <svg v-if="!photos.frontId && !loading.frontId" width="24" height="24"
                                    viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2"
                                    class="text-gray-400">
                                    <rect x="3" y="3" width="18" height="18" rx="2" ry="2" />
                                    <circle cx="8.5" cy="8.5" r="1.5" />
                                    <polyline points="21,15 16,10 5,21" />
                                </svg>
                                <div v-else-if="loading.frontId" class="flex items-center justify-center">
                                    <div class="animate-spin rounded-full h-6 w-6 border-b-2 border-purple-600"></div>
                                </div>
                                <img v-else :src="photos.frontId" alt="Front ID"
                                    class="w-full h-full object-cover rounded-lg" />
                            </div>

                            <!-- Camera Button -->
                            <button @click="takePhoto('frontId')" :disabled="loading.frontId" :class="[
                                'absolute -bottom-1 -right-1 w-7 h-7 rounded-full flex items-center justify-center transition-all duration-200 shadow-sm',
                                loading.frontId
                                    ? 'bg-gray-400 cursor-not-allowed'
                                    : 'bg-purple-600 hover:bg-purple-700 hover:scale-110'
                            ]">
                                <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                                    stroke-width="2" class="text-white">
                                    <path
                                        d="M23 19a2 2 0 0 1-2 2H3a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h4l2-3h6l2 3h4a2 2 0 0 1 2 2z" />
                                    <circle cx="12" cy="13" r="4" />
                                </svg>
                            </button>
                        </div>

                        <div class="flex-1 min-w-0">
                            <h3 class="font-semibold text-gray-900 text-sm sm:text-base">Front ID Card</h3>
                            <p class="text-xs text-gray-500 mt-1">National ID, Passport, or Driver's License</p>
                            <p v-if="photos.frontId" class="text-xs text-green-600 mt-1">✓ Uploaded successfully</p>
                            <p v-else class="text-xs text-gray-400 mt-1">Tap to upload or drag & drop</p>
                        </div>

                        <div v-if="photos.frontId" class="text-green-600 flex-shrink-0">
                            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                                stroke-width="2">
                                <path d="M22 11.08V12a10 10 0 1 1-5.93-9.14" />
                                <polyline points="22,4 12,14.01 9,11.01" />
                            </svg>
                        </div>
                    </div>
                </div>

                <!-- Back ID Card -->
                <div class="border border-gray-200 rounded-xl p-4 bg-white shadow-sm hover:shadow-md transition-shadow">
                    <div class="flex flex-col sm:flex-row sm:items-center gap-4">
                        <div class="relative flex-shrink-0">
                            <div class="w-20 h-20 sm:w-16 sm:h-16 bg-gray-50 rounded-xl flex items-center justify-center border-2 border-dashed border-gray-300 hover:border-purple-400 transition-colors cursor-pointer"
                                @click="openFileInput('backId')" @dragover.prevent="handleDragOver"
                                @drop.prevent="handleDrop($event, 'backId')" @dragenter.prevent="handleDragEnter"
                                @dragleave.prevent="handleDragLeave">

                                <!-- File Input (Hidden) -->
                                <input ref="backIdInput" type="file" accept="image/*" class="hidden"
                                    @change="handleFileSelect($event, 'backId')" />

                                <svg v-if="!photos.backId && !loading.backId" width="24" height="24" viewBox="0 0 24 24"
                                    fill="none" stroke="currentColor" stroke-width="2" class="text-gray-400">
                                    <rect x="3" y="3" width="18" height="18" rx="2" ry="2" />
                                    <circle cx="8.5" cy="8.5" r="1.5" />
                                    <polyline points="21,15 16,10 5,21" />
                                </svg>
                                <div v-else-if="loading.backId" class="flex items-center justify-center">
                                    <div class="animate-spin rounded-full h-6 w-6 border-b-2 border-purple-600"></div>
                                </div>
                                <img v-else :src="photos.backId" alt="Back ID"
                                    class="w-full h-full object-cover rounded-lg" />
                            </div>

                            <!-- Camera Button -->
                            <button @click="takePhoto('backId')" :disabled="loading.backId" :class="[
                                'absolute -bottom-1 -right-1 w-7 h-7 rounded-full flex items-center justify-center transition-all duration-200 shadow-sm',
                                loading.backId
                                    ? 'bg-gray-400 cursor-not-allowed'
                                    : 'bg-purple-600 hover:bg-purple-700 hover:scale-110'
                            ]">
                                <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                                    stroke-width="2" class="text-white">
                                    <path
                                        d="M23 19a2 2 0 0 1-2 2H3a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h4l2-3h6l2 3h4a2 2 0 0 1 2 2z" />
                                    <circle cx="12" cy="13" r="4" />
                                </svg>
                            </button>
                        </div>

                        <div class="flex-1 min-w-0">
                            <h3 class="font-semibold text-gray-900 text-sm sm:text-base">Back ID Card</h3>
                            <p class="text-xs text-gray-500 mt-1">Reverse side of your ID document</p>
                            <p v-if="photos.backId" class="text-xs text-green-600 mt-1">✓ Uploaded successfully</p>
                            <p v-else class="text-xs text-gray-400 mt-1">Tap to upload or drag & drop</p>
                        </div>

                        <div v-if="photos.backId" class="text-green-600 flex-shrink-0">
                            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                                stroke-width="2">
                                <path d="M22 11.08V12a10 10 0 1 1-5.93-9.14" />
                                <polyline points="22,4 12,14.01 9,11.01" />
                            </svg>
                        </div>
                    </div>
                </div>

                <!-- Selfie with Photo -->
                <div class="border border-gray-200 rounded-xl p-4 bg-white shadow-sm hover:shadow-md transition-shadow">
                    <div class="flex flex-col sm:flex-row sm:items-center gap-4">
                        <div class="relative flex-shrink-0">
                            <div class="w-20 h-20 sm:w-16 sm:h-16 bg-gray-50 rounded-xl flex items-center justify-center border-2 border-dashed border-gray-300 hover:border-purple-400 transition-colors cursor-pointer"
                                @click="openFileInput('selfie')" @dragover.prevent="handleDragOver"
                                @drop.prevent="handleDrop($event, 'selfie')" @dragenter.prevent="handleDragEnter"
                                @dragleave.prevent="handleDragLeave">

                                <!-- File Input (Hidden) -->
                                <input ref="selfieInput" type="file" accept="image/*" class="hidden"
                                    @change="handleFileSelect($event, 'selfie')" />

                                <svg v-if="!photos.selfie && !loading.selfie" width="24" height="24" viewBox="0 0 24 24"
                                    fill="none" stroke="currentColor" stroke-width="2" class="text-gray-400">
                                    <rect x="3" y="3" width="18" height="18" rx="2" ry="2" />
                                    <circle cx="8.5" cy="8.5" r="1.5" />
                                    <polyline points="21,15 16,10 5,21" />
                                </svg>
                                <div v-else-if="loading.selfie" class="flex items-center justify-center">
                                    <div class="animate-spin rounded-full h-6 w-6 border-b-2 border-purple-600"></div>
                                </div>
                                <img v-else :src="photos.selfie" alt="Selfie"
                                    class="w-full h-full object-cover rounded-lg" />
                            </div>

                            <!-- Camera Button -->
                            <button @click="takePhoto('selfie')" :disabled="loading.selfie" :class="[
                                'absolute -bottom-1 -right-1 w-7 h-7 rounded-full flex items-center justify-center transition-all duration-200 shadow-sm',
                                loading.selfie
                                    ? 'bg-gray-400 cursor-not-allowed'
                                    : 'bg-purple-600 hover:bg-purple-700 hover:scale-110'
                            ]">
                                <svg width="14" height="14" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                                    stroke-width="2" class="text-white">
                                    <path
                                        d="M23 19a2 2 0 0 1-2 2H3a2 2 0 0 1-2-2V8a2 2 0 0 1 2-2h4l2-3h6l2 3h4a2 2 0 0 1 2 2z" />
                                    <circle cx="12" cy="13" r="4" />
                                </svg>
                            </button>
                        </div>

                        <div class="flex-1 min-w-0">
                            <h3 class="font-semibold text-gray-900 text-sm sm:text-base">Selfie with ID</h3>
                            <p class="text-xs text-gray-500 mt-1">Hold your ID next to your face</p>
                            <p v-if="photos.selfie" class="text-xs text-green-600 mt-1">✓ Uploaded successfully</p>
                            <p v-else class="text-xs text-gray-400 mt-1">Tap to upload or drag & drop</p>
                        </div>

                        <div v-if="photos.selfie" class="text-green-600 flex-shrink-0">
                            <svg width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                                stroke-width="2">
                                <path d="M22 11.08V12a10 10 0 1 1-5.93-9.14" />
                                <polyline points="22,4 12,14.01 9,11.01" />
                            </svg>
                        </div>
                    </div>
                </div>
            </div>

            <!-- Tips Section -->
            <div class="mt-6 p-4 bg-blue-50 border border-blue-200 rounded-xl">
                <h4 class="font-semibold text-blue-900 text-sm mb-2">📸 Photo Tips</h4>
                <ul class="text-xs text-blue-800 space-y-1">
                    <li>• Ensure good lighting and clear focus</li>
                    <li>• Make sure all text is readable</li>
                    <li>• Avoid shadows and glare</li>
                    <li>• Keep your face clearly visible in selfie</li>
                </ul>
            </div>

            <!-- Continue Button -->
            <div class="mt-8">
                <button @click="handleContinue" :disabled="!isAllPhotosUploaded || isSubmitting || verificationSuccess"
                    :class="[
                        'w-full flex items-center justify-center gap-2 px-6 py-4 rounded-xl font-semibold text-white transition-all duration-200 shadow-sm',
                        isAllPhotosUploaded && !isSubmitting && !verificationSuccess
                            ? 'bg-purple-600 hover:bg-purple-700 hover:shadow-md active:scale-95'
                            : 'bg-gray-300 cursor-not-allowed'
                    ]">
                    <div v-if="isSubmitting" class="animate-spin rounded-full h-5 w-5 border-b-2 border-white"></div>
                    <svg v-else-if="!verificationSuccess" width="20" height="20" viewBox="0 0 24 24" fill="none"
                        stroke="currentColor" stroke-width="2">
                        <path d="M5 12h14M12 5l7 7-7 7" />
                    </svg>
                    <svg v-else width="20" height="20" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                        stroke-width="2" class="text-green-400">
                        <path d="M22 11.08V12a10 10 0 1 1-5.93-9.14" />
                        <polyline points="22,4 12,14.01 9,11.01" />
                    </svg>
                    {{
                        verificationSuccess
                            ? 'Verification Complete!'
                            : isSubmitting
                                ? 'Verifying Documents...'
                                : 'Continue to Verification'
                    }}
                </button>

                <!-- Retry Button (shown on error) -->
                <button v-if="verificationError && !isSubmitting" @click="handleContinue"
                    class="w-full mt-3 flex items-center justify-center gap-2 px-6 py-3 rounded-xl font-semibold text-purple-600 bg-purple-50 border border-purple-200 hover:bg-purple-100 transition-all duration-200">
                    <svg width="16" height="16" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                        <path d="M3 12a9 9 0 0 1 9-9 9.75 9.75 0 0 1 6.74 2.74L21 8" />
                        <path d="M21 3v5h-5" />
                        <path d="M21 12a9 9 0 0 1-9 9 9.75 9.75 0 0 1-6.74-2.74L3 16" />
                        <path d="M3 21v-5h5" />
                    </svg>
                    Try Again
                </button>
            </div>
        </div>
    </div>
</template>

<script setup>
import { ref, computed, nextTick } from 'vue'

// Props
const props = defineProps({
    loanData: {
        type: Object,
        default: null
    }
})

const photos = ref({
    frontId: null,
    backId: null,
    selfie: null
})

const loading = ref({
    frontId: false,
    backId: false,
    selfie: false
})

const isSubmitting = ref(false)

// Verification states
const verificationSuccess = ref(false)
const verificationError = ref(null)

// File input refs
const frontIdInput = ref(null)
const backIdInput = ref(null)
const selfieInput = ref(null)

const isKYCReady = computed(() => {
    return photos.value.frontId && photos.value.backId && photos.value.selfie
})

const isAllPhotosUploaded = computed(() => {
    return photos.value.frontId && photos.value.backId && photos.value.selfie
})

const uploadedCount = computed(() => {
    return Object.values(photos.value).filter(photo => photo !== null).length
})

// File handling functions
const openFileInput = (type) => {
    const inputRef = {
        frontId: frontIdInput,
        backId: backIdInput,
        selfie: selfieInput
    }[type]

    if (inputRef.value) {
        inputRef.value.click()
    }
}

const handleFileSelect = async (event, type) => {
    const file = event.target.files[0]
    if (!file) return

    await processFile(file, type)
    // Reset input value to allow selecting the same file again
    event.target.value = ''
}

const handleDragOver = (event) => {
    event.preventDefault()
    event.currentTarget.classList.add('border-purple-500', 'bg-purple-50')
}

const handleDragEnter = (event) => {
    event.preventDefault()
    event.currentTarget.classList.add('border-purple-500', 'bg-purple-50')
}

const handleDragLeave = (event) => {
    event.preventDefault()
    event.currentTarget.classList.remove('border-purple-500', 'bg-purple-50')
}

const handleDrop = async (event, type) => {
    event.preventDefault()
    event.currentTarget.classList.remove('border-purple-500', 'bg-purple-50')

    const files = event.dataTransfer.files
    if (files.length > 0) {
        await processFile(files[0], type)
    }
}

const processFile = async (file, type) => {
    // Validate file type
    if (!file.type.startsWith('image/')) {
        alert('Please select an image file')
        return
    }

    // Validate file size (max 5MB)
    if (file.size > 5 * 1024 * 1024) {
        alert('File size must be less than 5MB')
        return
    }

    loading.value[type] = true

    try {
        // Convert file to base64
        const base64 = await fileToBase64(file)
        photos.value[type] = base64

        console.log(`File uploaded successfully for ${type}`)
    } catch (error) {
        console.error(`Error processing file for ${type}:`, error)
        alert('Error processing file. Please try again.')
    } finally {
        loading.value[type] = false
    }
}

const fileToBase64 = (file) => {
    return new Promise((resolve, reject) => {
        const reader = new FileReader()
        reader.readAsDataURL(file)
        reader.onload = () => resolve(reader.result)
        reader.onerror = error => reject(error)
    })
}

const takePhoto = async (type) => {
    loading.value[type] = true
    try {
        // Check if device has camera access
        if (navigator.mediaDevices && navigator.mediaDevices.getUserMedia) {
            // In a real app, you would open camera here
            console.log(`Opening camera for ${type}`)

            // For demo purposes, we'll simulate a photo capture
            await new Promise(resolve => setTimeout(resolve, 1000))

            // Simulate a photo upload with a more realistic base64 image
            const mockImageData = 'data:image/jpeg;base64,/9j/4AAQSkZJRgABAQAAAQABAAD/2wBDAAYEBQYFBAYGBQYHBwYIChAKCgkJChQODwwQFxQYGBcUFhYaHSUfGhsjHBYWICwgIyYnKSopGR8tMC0oMCUoKSj/2wBDAQcHBwoIChMKChMoGhYaKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCgoKCj/wAARCAABAAEDASIAAhEBAxEB/8QAFQABAQAAAAAAAAAAAAAAAAAAAAv/xAAUEAEAAAAAAAAAAAAAAAAAAAAA/8QAFQEBAQAAAAAAAAAAAAAAAAAAAAX/xAAUEQEAAAAAAAAAAAAAAAAAAAAA/9oADAMBAAIRAxAAPwCdABmX/9k='

            photos.value[type] = mockImageData
            console.log(`Photo captured successfully for ${type}`)
        } else {
            // Fallback to file input if camera not available
            openFileInput(type)
        }
    } catch (error) {
        console.error(`Error capturing photo for ${type}:`, error)
        // Fallback to file input
        openFileInput(type)
    } finally {
        loading.value[type] = false
    }
}

const getFileSize = (photo) => {
    if (!photo) return '0KB'
    // In a real app, you'd calculate actual file size
    // For now, return a realistic mock size
    return '2.5KB'
}

const handleContinue = async () => {
    if (!isAllPhotosUploaded.value) {
        console.warn('Not all photos are uploaded yet')
        return
    }

    // Reset previous states
    verificationSuccess.value = false
    verificationError.value = null
    isSubmitting.value = true

    try {
        console.log('Starting KYC verification process...')

        // Validate all photos are present
        const validationErrors = []

        if (!photos.value.frontId) {
            validationErrors.push('Front ID photo is required')
        }
        if (!photos.value.backId) {
            validationErrors.push('Back ID photo is required')
        }
        if (!photos.value.selfie) {
            validationErrors.push('Selfie photo is required')
        }

        if (validationErrors.length > 0) {
            throw new Error(`Validation failed: ${validationErrors.join(', ')}`)
        }

        // Simulate API call for KYC verification
        console.log('Submitting KYC photos for verification...')

        // Simulate processing time (2-3 seconds)
        await new Promise(resolve => setTimeout(resolve, 2000 + Math.random() * 1000))

        // Simulate verification success (in real app, this would be API response)
        const verificationResult = {
            status: 'success',
            verificationId: 'KYC_' + Date.now(),
            timestamp: new Date().toISOString(),
            documents: {
                frontId: { status: 'verified', confidence: 0.95 },
                backId: { status: 'verified', confidence: 0.92 },
                selfie: { status: 'verified', confidence: 0.88 }
            },
            overallStatus: 'approved'
        }

        console.log('KYC verification completed successfully:', verificationResult)

        // Show success state
        verificationSuccess.value = true

        // Show success message briefly before navigation
        await new Promise(resolve => setTimeout(resolve, 1500))

        // Store data in localStorage for the identification page
        const kycData = {
            photos: photos.value,
            verification: verificationResult
        }
        localStorage.setItem('kycData', JSON.stringify(kycData))

        // Also store loan data if available (passed from parent component)
        if (props.loanData) {
            localStorage.setItem('loanData', JSON.stringify(props.loanData))
        }

        // Emit completion event with verification data
        emit('kyc-complete', kycData)

        console.log('KYC submission completed successfully')

        // Don't navigate directly - let parent handle the flow
        // await navigateTo('/identification')

    } catch (error) {
        console.error('Error during KYC verification:', error)

        // Handle different types of errors
        let errorMessage = 'Verification failed. Please try again.'

        if (error.message.includes('Validation failed')) {
            errorMessage = error.message
        } else if (error.message.includes('network') || error.message.includes('fetch')) {
            errorMessage = 'Network error. Please check your connection and try again.'
        } else if (error.message.includes('timeout')) {
            errorMessage = 'Request timed out. Please try again.'
        }

        // Set error state
        verificationError.value = errorMessage

        // Auto-clear error after 5 seconds
        setTimeout(() => {
            verificationError.value = null
        }, 5000)

    } finally {
        isSubmitting.value = false
    }
}

const emit = defineEmits(['back', 'kyc-complete'])
</script>

<style scoped>
/* Custom scrollbar for webkit browsers */
::-webkit-scrollbar {
    width: 6px;
}

::-webkit-scrollbar-track {
    background: #f1f1f1;
    border-radius: 3px;
}

::-webkit-scrollbar-thumb {
    background: #c7d2fe;
    border-radius: 3px;
}

::-webkit-scrollbar-thumb:hover {
    background: #a5b4fc;
}

/* Smooth transitions for all interactive elements */
* {
    transition: all 0.2s ease-in-out;
}

/* Focus styles for accessibility */
button:focus,
input:focus {
    outline: 2px solid #8b5cf6;
    outline-offset: 2px;
}

/* Hover effects for better UX */
.hover\:scale-110:hover {
    transform: scale(1.1);
}

.active\:scale-95:active {
    transform: scale(0.95);
}
</style>
