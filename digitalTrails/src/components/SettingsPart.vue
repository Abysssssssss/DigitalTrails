<template>
	<div class="main_block">
		<div class="settingsPart_field">
			<p id="settingsPart_field_p">Почта</p>
			<textarea name="" id="settingsPart_field_textArea"></textarea>
			<div id="ettingsPart_filed_images">
				<img class="base_style_img" src="../assets/icons/pencil--change-edit-modify-pencil-write-writing.svg"></img>
			</div>
		</div>
		<div class="settingsPart_field">
			<p id="settingsPart_field_p">Пароль</p>
			<textarea name="" id="settingsPart_field_textArea"></textarea>
			<div id="settingsPart_filed_images">
				<img class="base_style_img" id="settingsPart_img" src="../assets/icons/visible--eye-eyeball-open-view.svg" />
				<img class="base_style_img" id="settingsPart_img" src="../assets/icons/pencil--change-edit-modify-pencil-write-writing.svg" />
			</div>
		</div>
		<div class="settingsPart_field">
			<div class="settingsPart_switch_block">
				<p id="settingsPart_field_p">Отправлять новости и рекламные рекомендации на почту</p>
				<label class="switch">
					<input type="checkbox">
					<span class="slider round"></span>
				</label>
			</div>
		</div>
		<div class="settingsPart_field">
			<div class="settingsPart_switch_block">
				<p id="settingsPart_field_p">Хз что-то включить</p>
				<label class="switch">
					<input type="checkbox">
					<span class="slider round"></span>
				</label>
			</div>
		</div>
		<button id="settingsPart_button_exit">
			ВЫЙТИ
		</button>
	</div>
</template>
