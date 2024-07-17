<script setup>
import { ref } from 'vue';

const currencies = ref(['RUB', 'Другие валюты']);
const paymentMethods = ref([
	{ name: 'Картой РФ', commission: '8%' },
	{ name: 'Картой МИР', commission: '8%' },
	{ name: 'СБП', commission: '8%' },
	{ name: 'Payeer', commission: '8%' },
	{ name: 'SteamPay', commission: '8%' },
	{ name: 'Мегафон', commission: '8%' },
	{ name: 'Билайн', commission: '8%' },
	{ name: 'Tele2', commission: '8%' },
	{ name: 'PayPal', commission: '8%' },
	{ name: 'Stripe', commission: '8%' },
	{ name: 'FKWallet', commission: '8%' },
	{ name: 'Lava', commission: '8%' },
	{ name: 'Volet', commission: '8%' },
	{ name: 'PerfectMoney', commission: '8%' },
	{ name: 'Другой', commission: '8%' },
]);
const amounts = ref(['1.000₽', '2.000₽', '5.000₽', '10.000₽', '20.000₽', '50.000₽']);
</script>

<template>
	<div class="container">
		<h1 class="main-title">
			Пополните баланс,
			<span class="subtitle">чтобы получить номер для приема смс</span>
		</h1>
		<div class="mb-4">
			<div class="section-header">
				<h2 class="section-title">Выберите валюту оплаты</h2>
				<div class="icon-container">
					<img src="./assets/question-icon.svg" class="question-icon" alt="question-icon">
					<div class="tooltip">
						<p>Тут выбирается способ которым вы будете оплачивать</p>
					</div>
				</div>
			</div>
			<div class="button-group">
				<button v-for="currency in currencies" :key="currency" class="currency-button">
					{{ currency }}
				</button>
				<button class="currency-button">Криптовалюты</button>
			</div>
		</div>
		<div class="mb-4">
			<h2 class="text-lg font-semibold mb-2">Выберите способ оплаты</h2>
			<div class="grid grid-cols-3 gap-4">
				<div v-for="method in paymentMethods" :key="method.name" class="payment-method">
					<div class="font-semibold">{{ method.name }}</div>
					<div class="text-gray-500">Комиссия: {{ method.commission }}</div>
				</div>
			</div>
		</div>
		<div class="mb-4">
			<h2 class="text-lg font-semibold mb-2">Укажите сумму платежа</h2>
			<input type="text" placeholder="Минимальная сумма платежа: 1.000₽" class="payment-input" />
			<div class="button-group">
				<button v-for="amount in amounts" :key="amount" class="amount-button">
					{{ amount }}
				</button>
			</div>
		</div>
		<button class="custom-button">Оплатить</button>
	</div>
</template>

<style scoped>
@import './style.css';

.container {
	padding: 40px 0 80px 0;
}

.main-title {
	font-weight: bold;
	font-size: 2.25rem;
	line-height: 1.25;
	color: #1a202c;
	margin-bottom: 30px;
}

.subtitle {
	font-weight: 500;
	color: rgba(33, 37, 41, 0.6);
}

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

.button-group {
	display: flex;
	gap: 1rem;
}

.currency-button,
.amount-button {
	padding: 8px;
	background-color: #edf2f7;
	border-radius: 0.375rem;
}

.payment-method {
	padding: 16px;
	border: 1px solid #e2e8f0;
	border-radius: 0.375rem;
	text-align: center;
}

.payment-input {
	padding: 8px;
	border: 1px solid #e2e8f0;
	border-radius: 0.375rem;
	width: 100%;
	margin-bottom: 8px;
}

.custom-button {
	width: 100%;
	height: 4rem;
	border-radius: 0.5rem;
	padding: 0 1.25rem;
	font-weight: 500;
	color: #fff;
	background: linear-gradient(to right, #e2c299, #c5a67c);
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
</style>
