<template>
	<button @click="toggleTheme" class="theme_switcher">
		<p id="theme_switcher_span">
			{{ theme === 'light' ? '☀️' : '🌑' }}
		</p>
	</button>
</template>

<script>
export default {
	name: 'ThemeSwitcher',
	data() {
		return {
			theme: 'light',
		}
	},

	mounted() {
		const savedTheme = localStorage.getItem('theme')

		if (savedTheme) {
			this.theme = savedTheme
		} else {
			const prefersDark = window.matchMedia(
				'(prefers-color-scheme: dark)'
			).matches
			this.theme = prefersDark ? 'dark' : 'light'
		}

		this.setTheme(this.theme)
	},

	methods: {
		toggleTheme() {
			this.theme = this.theme === 'light' ? 'dark' : 'light'
			this.setTheme(this.theme)
			localStorage.setItem('theme', this.theme) // Сохраняем выбор
		},

		setTheme(theme) {
			document.documentElement.setAttribute('data-theme', theme)
		},
	},
}
</script>
