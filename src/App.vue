<script setup>
import {ref, watch} from 'vue';

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

const showInfo = ref(false)

const toggleInfo = () => {
	showInfo.value = !showInfo.value
}

const isActive = ref(false);
const hasError = ref(false);
const inputValue = ref('');

const clearInput = () => {
	inputValue.value = '';
	hasError.value = false;
};

const handleBlur = () => {
	isActive.value = false;
	validateInput();
};

const handleInput = (event) => {
	let value = event.target.value.replace(/[^\d]/g, ''); // Remove all non-digit characters
	inputValue.value = value ? `${parseInt(value).toLocaleString()}₽` : '';
};

const validateInput = () => {
	const numericValue = parseInt(inputValue.value.replace(/[^\d]/g, '')); // Extract numeric value

	hasError.value = numericValue < 1000;
};

watch(inputValue, (newValue) => {
	if (!newValue) {
		hasError.value = false;
	}
});
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
				<span class="currency-button">RUB</span>
				<div class="currency-button">
					<img src="" alt="">
					<p>Другие валюты</p>
					<img src="" alt="">
				</div>
				<button class="currency-button">Криптовалюты</button>
			</div>
		</div>
		<div class="mb-4">
			<h2 class="text-lg font-semibold mb-2">Выберите способ оплаты</h2>
			<div class="grid grid-cols-3 gap-4 mb-[15px]">
				<div v-for="method in paymentMethods" :key="method.name" class="payment-method">
					<img src="" alt="">
					<div>
						<div class="font-semibold">{{ method.name }}</div>
						<div class="text-gray-500">Комиссия: {{ method.commission }}</div>
					</div>
				</div>
			</div>
			<div @click="toggleInfo" class="flex w-[469px] mb-2 cursor-pointer items-center">
				<img src="./assets/warning-icon.svg" alt="warning-icon">
				<p class="text-[14px] mb-0 mx-1">Внимание, при нажатии раскрывается информация про страны</p>
				<img :class="{'rotate-180': showInfo, 'rotate-0': !showInfo}" class="transition-transform duration-300" src="./assets/arrow-icon.svg" alt="arrow-icon">
			</div>
			<div v-if="showInfo" class="payments-info">
				<p>Зачисление до 6 минут</p>
				<p>Эта платежная система не принимает платежи из стран:</p>
				<p>Армения, Австрия, Азербайджан, Бельгия, Болгария, Кипр, Чешская Республика, Дания, Эстония,
					Финляндия, Франция, Грузия, Германия, Греция, Венгрия, Исландия, Ирландия, Испания, Италия,
					Кыргызстан, Латвия, Литва, Люксембург, Мальта, Румыния, Сербия и Черногория, Словакия, Словения,
					Швеция, Швейцария, Таджикистан, Турция, Туркменистан, Соединенное Королевство, Узбекистан,
					Австралия, Норвегия, Израиль, Португалия, Нидерланды, Саудовская Аравия, Объединенные Арабские
					Эмираты, Сингапур, Новая Зеландия, Хорватия, Польша, Бруней-Даруссалам, Перу, Южная Корея, Катар,
					Египет.</p>
			</div>
		</div>
		<div class="mb-4">
			<h2 class="text-lg font-semibold mb-2">Укажите сумму платежа</h2>
			<div>
				<div class="input-group">
					<input
							type="text"
							placeholder="Минимальная сумма платежа: 1.000₽"
							class="payment-input"
							:class="{'active': isActive, 'error': hasError}"
							v-model="inputValue"
							@focus="isActive = true"
							@blur="handleBlur"
							@input="handleInput"
					/>
					<button v-if="inputValue" @click="clearInput" class="clear-button">✕</button>
				</div>
				<div v-if="hasError" class="error-message">
					Внимание, минимальная сумма 1.000₽
				</div>
			</div>
			<div v-if="hasError" class="error-message">
				Внимание, минимальная сумма 1.000₽
			</div>
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

.grid {
	max-height: 242px;
	overflow-y: auto;
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

.button-group {
	display: flex;
	gap: 8px; /* Adjust the gap between buttons if needed */
}

.amount-button {
	border-radius: 10px;
	padding: 8px 12px;
	width: 70px;
	height: 32px;
	background: rgba(33, 37, 41, 0.04);
	font-weight: 500;
	font-size: 14px;
	color: rgba(33, 37, 41, 0.6);
	border: none; /* Remove default border */
	cursor: pointer; /* Add pointer cursor on hover */
	display: flex;
	align-items: center;
	justify-content: center;
}

.amount-button:hover {
	border: 2px solid #E2C299;
}

.input-group {
	position: relative;
	display: flex;
	align-items: center;
}

.payment-input {
	width: 100%;
	padding: 8px 12px;
	border-radius: 10px;
	border: 1px solid #ced4da;
	font-size: 14px;
	font-weight: 500;
	color: rgba(33, 37, 41, 0.6);
	background-color: rgba(33, 37, 41, 0.04);
	transition: border-color 0.3s, background-color 0.3s;
}

.payment-input.active {
	border: 2px solid #D4A053;
	background-color: rgba(255, 255, 255, 1);
	color: #212529;
}

.payment-input.error {
	border: 2px solid #ff4d4f;
	color: #ff4d4f;
}

.clear-button {
	position: absolute;
	right: 10px;
	background: none;
	border: none;
	font-size: 16px;
	cursor: pointer;
	color: #ced4da;
}

.clear-button:hover {
	color: #212529;
}

.error-message {
	color: #ff4d4f;
	font-size: 12px;
	margin-top: 5px;
}
</style>
