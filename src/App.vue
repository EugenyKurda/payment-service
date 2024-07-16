<script setup>
import {ref} from 'vue';

const currencies = ref(['RUB', 'Другие валюты']);
const paymentMethods = ref([
	{name: 'Картой РФ', commission: '8%'},
	{name: 'Картой МИР', commission: '8%'},
	{name: 'СБП', commission: '8%'},
	{name: 'Payeer', commission: '8%'},
	{name: 'SteamPay', commission: '8%'},
	{name: 'Мегафон', commission: '8%'},
	{name: 'Билайн', commission: '8%'},
	{name: 'Tele2', commission: '8%'},
	{name: 'PayPal', commission: '8%'},
	{name: 'Stripe', commission: '8%'},
	{name: 'FKWallet', commission: '8%'},
	{name: 'Lava', commission: '8%'},
	{name: 'Volet', commission: '8%'},
	{name: 'PerfectMoney', commission: '8%'},
	{name: 'Другой', commission: '8%'},
]);
const amounts = ref(['1.000₽', '2.000₽', '5.000₽', '10.000₽', '20.000₽', '50.000₽']);
</script>

<template>
	<div class="px-0 pt-10 pb-20">
		<h1 class="font-bold text-4xl leading-[117%] text-[#212529] mb-[30px]">
			Пополните баланс,
			<span class="font-medium text-[rgba(33,37,41,0.6)]">чтобы получить номер для приема смс</span>
		</h1>
		<div class="mb-4">
			<div class="flex items-center mb-[15px]">
				<h2 class="font-normal text-xl text-[#212529] mr-[9px]">Выберите валюту оплаты</h2>
				<img src="./assets/question-icon.svg" alt="question-icon">
			</div>
			<div class="flex space-x-4">
				<button v-for="currency in currencies" :key="currency" class="p-2 bg-gray-200 rounded">
					{{ currency }}
				</button>
				<button class="p-2 bg-gray-200 rounded">Криптовалюты</button>
			</div>
		</div>
		<div class="mb-4">
			<h2 class="text-lg font-semibold mb-2">Выберите способ оплаты</h2>
			<div class="grid grid-cols-3 gap-4">
				<div v-for="method in paymentMethods" :key="method.name" class="p-4 border rounded text-center">
					<div class="font-semibold">{{ method.name }}</div>
					<div class="text-gray-500">Комиссия: {{ method.commission }}</div>
				</div>
			</div>
		</div>
		<div class="mb-4">
			<h2 class="text-lg font-semibold mb-2">Укажите сумму платежа</h2>
			<input type="text" placeholder="Минимальная сумма платежа: 1.000₽" class="p-2 border rounded w-full mb-2"/>
			<div class="flex space-x-2">
				<button v-for="amount in amounts" :key="amount" class="p-2 bg-gray-200 rounded">
					{{ amount }}
				</button>
			</div>
		</div>
		<button class="custom-button">Оплатить</button>
	</div>
</template>

<style scoped>
.custom-button {
	width: 1160px;
	height: 63px;
	border-radius: 12px;
	padding: 20px;
	font-family: "Roboto", sans-serif;
	font-weight: 500;
	font-size: 20px;
	color: #fff;
	background: linear-gradient(260deg, #e2c299 5.64%, #c5a67c 94.29%);
}
</style>
