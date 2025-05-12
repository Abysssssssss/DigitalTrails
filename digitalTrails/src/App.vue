<script setup>
import { shallowRef, markRaw } from 'vue'
import MainPart from './components/MainPart.vue'
import HistoryPart from './components/HistoryPart.vue'
import ThemeSwitcher from './components/ThemeSwitcher.vue'
import QrDecoder from './components/QrDecoder.vue'
import PanelMenu from './components/PanelMenu.vue'
import SettingsPart from './components/SettingsPart.vue'
import AboutPart from './components/AboutPart.vue'

const components = markRaw({
	QrDecoder,
	HistoryPart,
	AboutPart,
	SettingsPart,
})

const activeComponent = shallowRef(components.QrDecoder)
</script>

<template>
	<header>
		<ThemeSwitcher />
	</header>

	<main>
		<component :is="activeComponent" />
	</main>

	<footer>
		<PanelMenu
			@navigate="componentName => (activeComponent = components[componentName])"
		/>
	</footer>
</template>

<script></script>
