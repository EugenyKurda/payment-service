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
	<div class="px-0 pt-10 pb-20">
		<h1 class="main-title">
			Пополните баланс,
			<span class="subtitle">чтобы получить номер для приема смс</span>
		</h1>
		<div class="mb-4">
			<div class="section-header">
				<h2 class="section-title">Выберите валюту оплаты</h2>
				<img src="./assets/question-icon.svg" alt="question-icon">
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
			<input type="text" placeholder="Минимальная сумма платежа: 1.000₽" class="payment-input"/>
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

.main-title {
	@apply font-bold text-4xl leading-snug text-gray-900 mb-8;
}

.subtitle {
	@apply font-medium text-[rgba(33,37,41,0.6)];
}

.section-header {
	@apply flex items-center mb-4;
}

.section-title {
	@apply font-normal text-xl text-gray-900 mr-2;
}

.button-group {
	@apply flex space-x-4;
}

.currency-button,
.amount-button {
	@apply p-2 bg-gray-200 rounded;
}

.payment-method {
	@apply p-4 border rounded text-center;
}

.payment-input {
	@apply p-2 border rounded w-full mb-2;
}

.custom-button {
	@apply w-full h-16 rounded-lg px-5 font-medium text-white bg-gradient-to-r from-[#e2c299] to-[#c5a67c];
}
</style>
