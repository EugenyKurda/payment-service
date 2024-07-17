<template>
	<div class="mb-4">
		<h2 class="text-lg font-semibold mb-2">Выберите способ оплаты</h2>
		<div class="grid grid-cols-5 gap-[12px] mb-[15px]">
			<div v-for="method in paymentMethods" :key="method.name" class="payment-method">
				<img src="../assets/beeline-icon.svg" :alt="method.name">
				<div class="ml-[12px]">
					<div class="font-semibold">{{ method.name }}</div>
					<div class="text-gray-500">Комиссия: {{ method.commission }}</div>
				</div>
			</div>
		</div>
		<div @click="toggleInfo" class="flex w-[469px] mb-2 cursor-pointer items-center">
			<img src="../assets/warning-icon.svg" alt="warning-icon">
			<p class="text-[14px] mb-0 mx-1">Внимание, при нажатии раскрывается информация про страны</p>
			<img :class="{'rotate-180': showInfo, 'rotate-0': !showInfo}" class="transition-transform duration-300" src="../assets/arrow-icon.svg" alt="arrow-icon">
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
</template>

<script setup>
import { ref } from 'vue';

const paymentMethods = ref([
	{name: 'Картой РФ', commission: '8%', imgUrl: '../assets/visa-mastercard.png'},
	{name: 'Картой МИР', commission: '8%', imgUrl: '../assets/visa-mastercard.png'},
	{name: 'СБП', commission: '8%', imgUrl: '../assets/visa-mastercard.png'},
	{name: 'Payeer', commission: '8%', imgUrl: '../assets/visa-mastercard.png'},
	{name: 'SteamPay', commission: '8%', imgUrl: '../assets/visa-mastercard.png'},
	{name: 'Мегафон', commission: '8%', imgUrl: '../assets/visa-mastercard.png'},
	{name: 'Билайн', commission: '8%', imgUrl: '../assets/visa-mastercard.png'},
	{name: 'Tele2', commission: '8%', imgUrl: '../assets/visa-mastercard.png'},
	{name: 'PayPal', commission: '8%', imgUrl: '../assets/visa-mastercard.png'},
	{name: 'Stripe', commission: '8%', imgUrl: '../assets/visa-mastercard.png'},
	{name: 'FKWallet', commission: '8%', imgUrl: '../assets/visa-mastercard.png'},
	{name: 'Lava', commission: '8%', imgUrl: '../assets/visa-mastercard.png'},
	{name: 'Volet', commission: '8%', imgUrl: '../assets/visa-mastercard.png'},
	{name: 'PerfectMoney', commission: '8%', imgUrl: '../assets/visa-mastercard.png'},
	{name: 'Другой', commission: '8%', imgUrl: '../assets/visa-mastercard.png'},
	{name: 'Lava', commission: '8%', imgUrl: '../assets/visa-mastercard.png'},
	{name: 'Volet', commission: '8%', imgUrl: '../assets/visa-mastercard.png'},
	{name: 'PerfectMoney', commission: '8%', imgUrl: '../assets/visa-mastercard.png'},
	{name: 'Другой', commission: '8%', imgUrl: '../assets/visa-mastercard.png'},
]);

const showInfo = ref(false);
const toggleInfo = () => {
	showInfo.value = !showInfo.value;
};
</script>

<style scoped>
@import '../style.css';

.grid {
	max-height: 242px;
	overflow-y: auto;
}

.payment-method {
	border-radius: 12px;
	padding: 14px 20px;
	width: 219px;
	height: 68px;
	display: flex;
	align-items: center;
}

.payment-method:hover {
	border: 2px solid #E2C299;
}

.flex {
	display: flex;
}

.items-center {
	align-items: center;
}

.cursor-pointer {
	cursor: pointer;
}

.mb-2 {
	margin-bottom: 0.5rem;
}

.mb-4 {
	margin-bottom: 1rem;
}

.rotate-180 {
	transform: rotate(180deg);
}

.rotate-0 {
	transform: rotate(0);
}

.transition-transform {
	transition: transform 0.3s;
}

.duration-300 {
	transition-duration: 0.3s;
}

.payments-info {
	background: #f8f9fa;
	padding: 10px;
	border-radius: 0.375rem;
	border: 1px solid #e2e8f0;
}
</style>
