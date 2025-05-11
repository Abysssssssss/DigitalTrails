<script setup>
import MainPart from './components/MainPart.vue'
import HistoryPart from './components/HistoryPart.vue'
import ThemeSwitcher from './components/ThemeSwitcher.vue'
import QrDecoder from './components/QrDecoder.vue'
import PanelMenu from './components/PanelMenu.vue'
</script>

<template>
	<header>
		<p id="app_header-text">ПАВЛОВСКИЙ</p>
		<ThemeSwitcher />
	</header>

	<main>
		<!-- <HistoryPart /> -->
		<QrDecoder />
		<!-- <MainPart /> -->
	</main>

	<footer></footer>
</template>

<script></script>
