<template>
	<div class="mb-4">
		<div class="section-header">
			<h2 class="section-title">Выберите валюту оплаты</h2>
			<div class="icon-container">
				<img src="../assets/question-icon.svg" class="question-icon" alt="question-icon">
				<div class="tooltip">
					<p>Тут выбирается способ которым вы будете оплачивать</p>
				</div>
			</div>
		</div>
		<div class="button-group">
			<div class="currency-button">
				<img src="../assets/rub-icon.svg" alt="RUB" class="currency-icon">
				<span>RUB</span>
			</div>
			<div class="currency-button flex-between">
				<img src="../assets/exchange.svg" alt="exchange" class="currency-icon">
				<span>Другие валюты</span>
				<img src="../assets/arrow-icon.svg" alt="arrow-icon" class="arrow-icon">
			</div>
		</div>
	</div>
</template>

<script setup>
import { ref } from 'vue';

const currencies = ref(['RUB', 'Другие валюты', 'Криптовалюты']);
</script>

<style scoped>
@import '../style.css';

.section-header {
	display: flex;
	align-items: center;
	margin-bottom: 15px;
}

.section-title {
	font-size: 1.25rem;
	color: #1a202c;
	margin-right: 8px;
}

.icon-container {
	position: relative;
	display: inline-block;
}

.question-icon {
	transition: background-color 0.3s, filter 0.3s;
}

.question-icon:hover {
	background-color: black;
	border-radius: 50%;
	filter: invert(1);
}

.tooltip {
	display: none;
	position: absolute;
	top: 20px;
	right: -360px;
	transform: translateX(-50%);
	color: black;
	text-align: start;
	box-shadow: 0 0 20px 0 rgba(0, 0, 0, 0.08);
	background: #fff;
	z-index: 1;
	border-radius: 0 10px 10px 10px;
	padding: 8px 12px;
	width: 247px;
	height: 56px;
}

.tooltip p {
	font-weight: 500;
	font-size: 14px;
	line-height: 1.43;
	color: #212529;
}

.icon-container:hover .tooltip {
	display: block;
}

.button-group {
	display: flex;
	gap: 16px;
}

.currency-button {
	display: flex;
	align-items: center;
	padding: 8px 16px;
	background-color: #fff;
	border: 1px solid #e2e8f0;
	border-radius: 8px;
	box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
	cursor: pointer;
	transition: background-color 0.3s, border-color 0.3s;
}

.currency-button:hover {
	border-color: #e2c299;
}

.flex-between {
	justify-content: space-between;
	width: 200px;
}

.currency-icon {
	width: 24px;
	height: 24px;
	margin-right: 8px;
}

.arrow-icon {
	margin-left: auto;
}
</style>

