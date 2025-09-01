<template>
	<div class="panel-container">
		<img
			id="panelMenu_icon"
			src="/icons/align-center.svg"
			@mousedown="startDrag"
			@touchstart="startDrag"
		/>

		<div class="panelMenu_wrapper" :style="{ height: panelHeight + 'px' }">
			<ul class="panelMenu_block">
				<li
					class="panelMenu_block_li"
					id="panelMenu_block_li_1"
					@click="navigate('QrDecoder')"
				>
					Главная
				</li>
				<li class="panelMenu_block_li" @click="navigate('HistoryPart')">
					Пути
				</li>
				<li class="panelMenu_block_li" @click="navigate('AboutPart')">
					О парке
				</li>
				<li
					class="panelMenu_block_li"
					id="panelMenu_block_li_2"
					@click="navigate('SettingsPart')"
				>
					Настройки
				</li>
			</ul>
		</div>
	</div>
</template>

<script>
export default {
	emits: ['navigate'],

	data() {
		return {
			panelHeight: 0,
			maxHeight: 60,
			isDragging: false,
			startY: 0,
		}
	},
	methods: {
		navigate(component) {
			this.$emit('navigate', component)
			this.panelHeight = 0
		},

		startDrag(e) {
			this.isDragging = true
			this.startY = e.clientY || e.touches[0].clientY
			if (e.touches) e.preventDefault()

			document.addEventListener('mousemove', this.drag)
			document.addEventListener('touchmove', this.drag, { passive: false })
			document.addEventListener('mouseup', this.stopDrag)
			document.addEventListener('touchend', this.stopDrag)
		},

		drag(e) {
			if (!this.isDragging) return
			const y = e.clientY || e.touches[0].clientY
			this.panelHeight = Math.min(this.maxHeight, Math.max(0, this.startY - y))
			if (e.cancelable) e.preventDefault()
		},

		stopDrag() {
			this.isDragging = false
			this.panelHeight =
				this.panelHeight > this.maxHeight / 2 ? this.maxHeight : 0
			document.removeEventListener('mousemove', this.drag)
			document.removeEventListener('touchmove', this.drag)
			document.removeEventListener('mouseup', this.stopDrag)
			document.removeEventListener('touchend', this.stopDrag)
		},
	},
}
</script>
