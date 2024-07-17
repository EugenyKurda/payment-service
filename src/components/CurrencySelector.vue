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
				<img src="../assets/btc.svg" alt="btc" class="currency-icon">
				<span>Криптовалюты</span>
			</div>
			<div class="currency-button">
				<div class="current-currency">
					<img src="../assets/rub-icon.svg" alt="RUB" class="currency-icon">
					<span>RUB</span>
				</div>
				<div class="choosing-currency" @click="toggleCurrencies">
					<img src="../assets/exchange.svg" alt="exchange" class="currency-icon">
					<span class="ml-[10px]">Другие валюты</span>
					<img :class="{'rotate-180': showCurrencies, 'ml-[10px]': true}" src="../assets/arrow-icon.svg" alt="arrow-icon">
				</div>
			</div>
		</div>
		<div v-if="showCurrencies" class="grid grid-cols-9 gap-[15px] mb-[15px] all-currents">
			<div class="current-element" v-for="method in 10" :key="method">
				<img src="../assets/rub-icon.svg" alt="RUB" class="currency-icon">
				<span>RUB</span>
			</div>
		</div>
	</div>
</template>

<script setup>
import { ref } from 'vue';

const showCurrencies = ref(false);
const toggleCurrencies = () => {
	showCurrencies.value = !showCurrencies.value;
};
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
	justify-content: space-between;
	border-radius: 12px;
	padding: 15px 24px 15px 20px;
	width: fit-content;
	height: 68px;
	box-shadow: 0 0 15px 0 rgba(0, 0, 0, 0.06);
	background: #fff;
}

.current-currency {
	display: flex;
	align-items: center;
	border-right: 1px solid rgba(0, 0, 0, 0.1);
	padding: 12px 20px 12px 16px;
	width: 107px;
	height: 52px;
	margin-right: 10px;
}

.choosing-currency {
	display: flex;
	align-items: center;
	cursor: pointer;
}

.currency-button:hover {
	border-color: #e2c299;
}

.currency-icon {
	width: 24px;
	height: 24px;
	margin-right: 8px;
}

.all-currents {
	width: 100%;
	max-height: 131px;
	height: 100%;
	overflow: auto;
}

.current-element {
	display: flex;
	align-items: center;
	border-radius: 12px;
	padding: 15px 24px 15px 20px;
	width: 111px;
	height: 58px;
}

.current-element:hover {
	border: 2px solid #E2C299;
}

.rotate-180 {
	transform: rotate(180deg);
	transition: transform 0.3s;
}
</style>


