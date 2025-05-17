<template>
	<div class="main-app">
	<!-- Логотип компании -->
	<button 
		class="section-btn with-logo" 
		@click="toggleSection('company')"
		:class="{ active: activeSection === 'company' }"
    >
	<div class="btn-content">
	<img src="@/assets/imageav1.png" alt="Company Logo" class="company-logo">
	<span>namecompany</span>
	</div>
	<span class="arrow">{{ activeSection === 'company' ? '▲' : '✧' }}</span>
</button>
	
	<!-- Контент Namecompany -->
	<div class="content-block" :class="{ active: activeSection === 'company' }">
	<p>Мы, компания "Оаоzim", занимаемся разработкой веб-приложений с акцентом на безопасность, удобство и эффективность.</p>
	<p>Мы тщательно анализируем требования клиентов и создаем интуитивно понятный дизайн, чтобы обеспечить комфорт пользователей. Используем современные технологии и лучшие практики для обеспечения надежности и высокой производительности наших решений. В процессе работы проводим тестирование и оптимизацию, чтобы исключить баги и повысить стабильность системы. Внедряем автоматизированные процессы развертывания и мониторинга для своевременного реагирования на любые проблемы. Наша цель — создавать качественные продукты, которые будут расти вместе с бизнесом наших клиентов.</p>
	</div>

	<!-- Кнопка Concept -->
	<button 
		class="section-btn" 
		@click="toggleSection('concept')"
		:class="{ active: activeSection === 'concept' }"
    >
	concept(idea)
	<span class="arrow">{{ activeSection === 'concept' ? '▲' : '✧' }}</span>
	</button>
	
	<!-- Контент Concept -->
	<div class="content-block" :class="{ active: activeSection === 'concept' }">
	<p>Мы, компания "Оаоzim", занимаемся разработкой веб-приложений с акцентом на безопасность, удобство и эффективность.</p>
	<p>Мы тщательно анализируем требования клиентов и создаем интуитивно понятный дизайн, чтобы обеспечить комфорт пользователей. Используем современные технологии и лучшие практики для обеспечения надежности и высокой производительности наших решений. В процессе работы проводим тестирование и оптимизацию, чтобы исключить баги и повысить стабильность системы. Внедряем автоматизированные процессы развертывания и мониторинга для своевременного реагирования на любые проблемы. Наша цель — создавать качественные продукты, которые будут расти вместе с бизнесом наших клиентов.</p>
	</div>

	<!-- Кнопка Role -->
	<button 
		class="section-btn" 
		@click="toggleSection('role')"
		:class="{ active: activeSection === 'role' }"
    >
	role
	<span class="arrow">{{ activeSection === 'role' ? '▲' : '✧' }}</span>
	</button>
	
	<!-- Контент Role -->
	<div class="content-block" :class="{ active: activeSection === 'role' }">
	<h2>Наша команда</h2>
	
	<div class="team-member">
		<img src="@/assets/imageav.png" alt="Павел" class="member-avatar">
		<div class="member-info">
		<h3>Павел</h3>
		<p>Разработчик и проектировщик интерфейса веб-приложения, работая как с фронтендом, так и с бэкендом, обеспечивая функциональность и удобство использования. Он отвечает за интеграцию дизайна и техническую реализацию всех элементов системы.</p>
		</div>
	</div>
	
	<div class="team-member">
		<img src="@/assets/imageav.png" alt="Илья" class="member-avatar">
		<div class="member-info">
		<h3>Илья</h3>
		<p>Разработчик фронтенда и бэкенда, создает визуальную часть сайта и обеспечивает его работу на серверной стороне. Он занимается реализацией пользовательских интерфейсов и интеграцией их с серверными компонентами.</p>
		</div>
	</div>
	
	<div class="team-member">
		<img src="@/assets/imageav.png" alt="Андрей" class="member-avatar">
		<div class="member-info">
		<h3>Андрей</h3>
		<p>Дизайнер, копирайтер и контент-менеджер, разрабатывает визуальные материалы, пишет тексты и управляет содержимым сайта для создания привлекательного и информативного пользовательского опыта.</p>
		</div>
	</div>
	</div>
	</div>
  </template>
  
  <script>
  export default {
	name: 'MainPart',
	data() {
	  return {
		activeSection: null
	  }
	},
	methods: {
	  toggleSection(section) {
		if (this.activeSection === section) {
		  this.activeSection = null;
		} else {
		  this.activeSection = section;
		}
	  }
	}
  }
  </script>
<style scoped>
/* Импортируем стили из отдельного файла */
@import './../assets/mainPart.css';
</style>
  