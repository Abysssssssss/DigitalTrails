<template>
	<div class="qrDecoder_cameraBlock">
		<qrcode-stream @detect="onDetect" :paused="paused" v-if="hasCameraAccess">
			<div class="scan-overlay"></div>
		</qrcode-stream>

		<div v-if="error" class="error">
			{{ error }}
		</div>
		<button class="start-button" @click="initCamera">Включить камеру</button>
	</div>
</template>

<script>
import { QrcodeStream } from 'vue-qrcode-reader'

export default {
	components: { QrcodeStream },
	data() {
		return {
			hasCameraAccess: false,
			paused: false,
			result: null,
			error: null,
		}
	},
	methods: {
		async initCamera() {
			try {
				// Проверка поддержки камеры
				const devices = await navigator.mediaDevices.enumerateDevices()
				const hasCamera = devices.some(device => device.kind === 'videoinput')

				if (!hasCamera) {
					throw new Error('Камера не найдена')
				}

				// Запрос разрешения
				await navigator.mediaDevices.getUserMedia({ video: true })
				this.hasCameraAccess = true
			} catch (err) {
				this.error = this.getErrorMessage(err)
			}
		},

		onDetect(detectedCodes) {
			if (detectedCodes.length > 0) {
				this.result = detectedCodes[0].rawValue
				this.paused = true // Останавливаем сканирование
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
}
</script>
