<template>
	<div class="qrDecoder_cameraBlock">
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
			class="duration-button"
			:class="{ active: cameraActive }"
			@click="toggleCamera"
		>
			{{ cameraActive ? 'Выключить камеру' : 'Включить камеру' }}
		</button>

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
			mediaStream: null, // Храним ссылку на поток камеры
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
				// Останавливаем предыдущий поток, если есть
				if (this.mediaStream) {
					this.stopCamera()
				}

				// Запрашиваем доступ к камере
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
				// Останавливаем все треки
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
		// Очищаем ресурсы при уничтожении компонента
		this.stopCamera()
	},
}
</script>
