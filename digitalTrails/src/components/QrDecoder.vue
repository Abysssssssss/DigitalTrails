<!-- QrDecoder.vue -->
<template>
    <div class="qr-scanner">
        <div class="instruction">Просканируйте QR code</div>

        <qrcode-stream
            @detect="onDetect"
            :paused="paused"
            v-if="cameraActive"
            @camera-on="onCameraOn"
            @camera-off="onCameraOff"
        >
            <div class="scan-overlay"></div>
        </qrcode-stream>

        <div v-if="error" class="error">
            {{ error }}
        </div>

        <button
            class="camera-button"
            :class="{ active: cameraActive }"
            @click="toggleCamera"
        >
            {{ cameraActive ? 'ВЫКЛ камера' : 'ВКЛ камера' }}
        </button>

        <div v-if="cameraActive" class="camera-status">
            Камера включена
        </div>
        <div v-else class="camera-status">
            Камера выключена
        </div>

        <div v-if="result" class="result">
            Найден код: {{ result }}
            <button @click="resetScanner">Сканировать ещё</button>
        </div>
    </div>
</template>

<script>
import { QrcodeStream } from 'vue-qrcode-reader'

export default {
    components: { QrcodeStream },
    data() {
        return {
            cameraActive: false,
            paused: false,
            result: null,
            error: null,
            mediaStream: null,
        }
    },
    methods: {
        async toggleCamera() {
            if (this.cameraActive) {
                await this.stopCamera()
            } else {
                await this.startCamera()
            }
        },

        async startCamera() {
            try {
                if (this.mediaStream) {
                    this.stopCamera()
                }

                this.mediaStream = await navigator.mediaDevices.getUserMedia({
                    video: {
                        facingMode: 'environment',
                        width: { ideal: 1280 },
                    },
                })

                this.cameraActive = true
                this.paused = false
                this.error = null
            } catch (err) {
                this.error = this.getErrorMessage(err)
                console.error('Camera error:', err)
            }
        },

        async stopCamera() {
            if (this.mediaStream) {
                this.mediaStream.getTracks().forEach(track => track.stop())
                this.mediaStream = null
            }
            this.cameraActive = false
            this.paused = true
        },

        onCameraOn() {
            console.log('Камера включена')
        },

        onCameraOff() {
            console.log('Камера выключена')
        },

        onDetect(detectedCodes) {
            if (detectedCodes.length > 0) {
                this.result = detectedCodes[0].rawValue
                this.paused = true
                console.log('Распознано:', this.result)
            }
        },

        resetScanner() {
            this.result = null
            this.paused = false
        },

        getErrorMessage(error) {
            if (error.name === 'NotAllowedError') {
                return 'Доступ к камере запрещён. Разрешите доступ в настройках браузера.'
            }
            return 'Ошибка: ' + error.message
        },
    },

    beforeUnmount() {
        this.stopCamera()
    },
}
</script>