<template>
    <div class="identification-container">
        <!-- Header -->
        <div class="header">
            <button class="back-button" @click="goBack">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" xmlns="http://www.w3.org/2000/svg">
                    <path d="M15 18L9 12L15 6" stroke="white" stroke-width="2" stroke-linecap="round"
                        stroke-linejoin="round" />
                </svg>
            </button>
            <h1 class="header-title">Verification Status</h1>
        </div>

        <!-- Status Message -->
        <div v-if="kycData" class="status-message">
            <div class="status-icon">
                <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <path d="M22 11.08V12a10 10 0 1 1-5.93-9.14" />
                    <polyline points="22,4 12,14.01 9,11.01" />
                </svg>
            </div>
            <p>Identity verification completed successfully</p>
        </div>

        <!-- Uploaded Documents -->
        <div v-if="kycData?.photos" class="identification-steps">
            <div class="step-item">
                <div class="image-placeholder">
                    <img v-if="kycData.photos.frontId" :src="kycData.photos.frontId" alt="Front ID card"
                        class="step-image" />
                    <div v-else class="placeholder-content">
                        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                            stroke-width="2">
                            <rect x="3" y="3" width="18" height="18" rx="2" ry="2" />
                            <circle cx="8.5" cy="8.5" r="1.5" />
                            <polyline points="21,15 16,10 5,21" />
                        </svg>
                    </div>
                </div>
                <div class="step-text">
                    <span>Front ID card</span>
                    <span v-if="kycData.photos.frontId" class="status-badge">✓ Uploaded</span>
                </div>
            </div>

            <div class="step-item">
                <div class="image-placeholder">
                    <img v-if="kycData.photos.backId" :src="kycData.photos.backId" alt="Back ID card"
                        class="step-image" />
                    <div v-else class="placeholder-content">
                        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                            stroke-width="2">
                            <rect x="3" y="3" width="18" height="18" rx="2" ry="2" />
                            <circle cx="8.5" cy="8.5" r="1.5" />
                            <polyline points="21,15 16,10 5,21" />
                        </svg>
                    </div>
                </div>
                <div class="step-text">
                    <span>Back ID card</span>
                    <span v-if="kycData.photos.backId" class="status-badge">✓ Uploaded</span>
                </div>
            </div>

            <div class="step-item">
                <div class="image-placeholder">
                    <img v-if="kycData.photos.selfie" :src="kycData.photos.selfie" alt="Selfie with photo"
                        class="step-image" />
                    <div v-else class="placeholder-content">
                        <svg width="24" height="24" viewBox="0 0 24 24" fill="none" stroke="currentColor"
                            stroke-width="2">
                            <rect x="3" y="3" width="18" height="18" rx="2" ry="2" />
                            <circle cx="8.5" cy="8.5" r="1.5" />
                            <polyline points="21,15 16,10 5,21" />
                        </svg>
                    </div>
                </div>
                <div class="step-text">
                    <span>Selfie with photo</span>
                    <span v-if="kycData.photos.selfie" class="status-badge">✓ Uploaded</span>
                </div>
            </div>
        </div>

        <!-- No Data Message -->
        <div v-else class="no-data-message">
            <div class="no-data-icon">
                <svg width="48" height="48" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2">
                    <rect x="3" y="3" width="18" height="18" rx="2" ry="2" />
                    <circle cx="8.5" cy="8.5" r="1.5" />
                    <polyline points="21,15 16,10 5,21" />
                </svg>
            </div>
            <p>No verification data available</p>
            <p class="subtitle">Complete KYC process to see verification status</p>
        </div>

        <!-- Continue Button -->
        <div class="continue-section">
            <button class="continue-button" @click="handleContinue" :disabled="!kycData">
                <svg class="send-icon" width="20" height="20" viewBox="0 0 24 24" fill="none"
                    xmlns="http://www.w3.org/2000/svg">
                    <path d="M22 2L11 13M22 2L15 22L11 13M22 2L2 9L11 13" stroke="white" stroke-width="2"
                        stroke-linecap="round" stroke-linejoin="round" />
                </svg>
                <span>{{ kycData ? 'VIEW DETAILS' : 'CONTINUE' }}</span>
            </button>
        </div>
    </div>
</template>

<script setup>
import { ref, onMounted } from 'vue'

const emit = defineEmits(['back', 'continue'])

// Reactive data
const kycData = ref(null)

const goBack = () => {
    emit('back')
}

const handleContinue = () => {
    if (kycData.value) {
        // Navigate to the identification page with data
        navigateTo('/identification')
    } else {
        emit('continue')
    }
}

onMounted(() => {
    // Get KYC data from localStorage
    const storedKycData = localStorage.getItem('kycData')
    if (storedKycData) {
        try {
            kycData.value = JSON.parse(storedKycData)
        } catch (error) {
            console.error('Error parsing KYC data:', error)
        }
    }
})
</script>

<style scoped>
.identification-container {
    min-height: 100vh;
    background-color: #f8f9fa;
    display: flex;
    flex-direction: column;
}

/* Header */
.header {
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    padding: 16px 20px;
    display: flex;
    align-items: center;
    position: relative;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
}

.back-button {
    background: none;
    border: none;
    padding: 8px;
    cursor: pointer;
    display: flex;
    align-items: center;
    justify-content: center;
}

.header-title {
    color: white;
    font-size: 18px;
    font-weight: 600;
    margin: 0;
    position: absolute;
    left: 50%;
    transform: translateX(-50%);
}

/* Status Message */
.status-message {
    padding: 20px;
    text-align: center;
    background: linear-gradient(135deg, #d1fae5 0%, #a7f3d0 100%);
    margin: 0 20px;
    border-radius: 12px;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 12px;
}

.status-message p {
    color: #065f46;
    font-size: 16px;
    margin: 0;
    font-weight: 500;
}

.status-icon {
    color: #059669;
}

/* No Data Message */
.no-data-message {
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    padding: 40px 20px;
    text-align: center;
}

.no-data-icon {
    color: #9ca3af;
    margin-bottom: 16px;
}

.no-data-message p {
    color: #6b7280;
    font-size: 16px;
    margin: 0 0 8px 0;
    font-weight: 500;
}

.no-data-message .subtitle {
    color: #9ca3af;
    font-size: 14px;
    font-weight: 400;
}

/* Identification Steps */
.identification-steps {
    flex: 1;
    padding: 0 20px;
    display: flex;
    flex-direction: column;
    gap: 16px;
}

.step-item {
    background: white;
    border-radius: 12px;
    padding: 16px;
    display: flex;
    align-items: center;
    gap: 16px;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
    border: 1px solid #e9ecef;
}

.image-placeholder {
    width: 80px;
    height: 80px;
    border-radius: 8px;
    overflow: hidden;
    background-color: #f8f9fa;
    display: flex;
    align-items: center;
    justify-content: center;
}

.step-image {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: 8px;
}

.placeholder-content {
    width: 100%;
    height: 100%;
    display: flex;
    align-items: center;
    justify-content: center;
    color: #9ca3af;
}

.step-text {
    flex: 1;
    display: flex;
    flex-direction: column;
    gap: 4px;
}

.step-text span {
    color: #333;
    font-size: 16px;
    font-weight: 500;
}

.status-badge {
    color: #059669;
    font-size: 12px;
    font-weight: 500;
}

/* Continue Section */
.continue-section {
    padding: 20px;
    background: white;
    border-top: 1px solid #e9ecef;
}

.continue-button {
    width: 100%;
    background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
    border: none;
    border-radius: 12px;
    padding: 16px 24px;
    color: white;
    font-size: 16px;
    font-weight: 600;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 12px;
    cursor: pointer;
    transition: all 0.3s ease;
    box-shadow: 0 4px 12px rgba(102, 126, 234, 0.3);
}

.continue-button:hover:not(:disabled) {
    transform: translateY(-2px);
    box-shadow: 0 6px 16px rgba(102, 126, 234, 0.4);
}

.continue-button:active:not(:disabled) {
    transform: translateY(0);
}

.continue-button:disabled {
    background: linear-gradient(135deg, #d1d5db 0%, #9ca3af 100%);
    cursor: not-allowed;
    transform: none;
    box-shadow: none;
}

.send-icon {
    width: 20px;
    height: 20px;
}

/* Responsive Design */
@media (max-width: 480px) {
    .header {
        padding: 12px 16px;
    }

    .instruction {
        padding: 16px;
    }

    .identification-steps {
        padding: 0 16px;
    }

    .step-item {
        padding: 12px;
    }

    .image-placeholder {
        width: 60px;
        height: 60px;
    }

    .continue-section {
        padding: 16px;
    }
}
</style>
