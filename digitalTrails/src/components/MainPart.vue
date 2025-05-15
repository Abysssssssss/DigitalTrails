<!-- MainPart.vue -->
<template>
	<div class="mainPart">
	  <div class="content">
		<div class="intro-text">
		  Добро пожаловать в Павловский парк - один из самых красивых парков России!
		</div>
  
		<div class="feed">
		  <!-- Текстовый блок -->
		  <div class="text-card">
			<h3>История парка</h3>
			<p>Павловский парк основан в конце XVIII века как летняя резиденция императора Павла I.</p>
		  </div>
  
		  <!-- Блок с изображением -->
		  <div class="image-card">
			<img src="@/assets/images/park1.jpg" alt="Павловский парк">
			<p class="image-caption">Вид на дворец с реки Славянки</p>
		  </div>
  
		  <!-- Текстовый блок -->
		  <div class="text-card">
			<h3>Архитектура</h3>
			<p>Парк создан в английском стиле с элементами регулярной планировки.</p>
		  </div>
  
		  <!-- Блок с изображением -->
		  <div class="image-card">
			<img src="@/assets/images/park2.jpg" alt="Павловский парк">
			<p class="image-caption">Мост Кентавров в Павловском парке</p>
		  </div>
  
		  <!-- Добавьте еще 6 подобных блоков (всего 10) -->
		</div>
	  </div>
	</div>
  </template>
  
  <script>
  export default {
	name: 'MainPart'
  }
  </script>