<template>
	<div class="mb-4">
		<h2 class="text-lg font-semibold mb-2">Выберите способ оплаты</h2>
		<div class="grid grid-cols-5 gap-[12px] mb-4 max-h-[242px] w-[100%] overflow-y-auto">
			<div v-for="method in paymentMethods" :key="method.name" class="payment-method flex items-center p-4 w-[219px] h-[68px] rounded-lg hover:border-2 hover:border-[#E2C299]">
				<img :src="method.imgUrl" :alt="method.name">
				<div class="ml-3">
					<div class="font-semibold">{{ method.name }}</div>
					<div class="text-gray-500">Комиссия: {{ method.commission }}</div>
				</div>
			</div>
		</div>
		<div @click="toggleInfo" class="flex w-[469px] mb-2 cursor-pointer items-center">
			<img src="../assets/warning-icon.svg" alt="warning-icon">
			<p class="text-[14px] font-medium text-[#212529] mb-0 mx-1">Внимание, при нажатии раскрывается информация про страны</p>
			<img :class="{'rotate-180': showInfo, 'rotate-0': !showInfo}" class="transition-transform duration-300 ml-1" src="../assets/arrow-icon.svg" alt="arrow-icon">
		</div>
		<div v-if="showInfo" class="payments-info bg-gray-100 p-2 rounded">
			<p class="text-[14px] leading-[143%] font-normal text-[#212529] mb-2">Зачисление до 6 минут</p>
			<p class="text-[14px] leading-[143%] font-normal text-[#212529] mb-0">Эта платежная система не принимает платежи из стран:</p>
			<p class="text-[14px] leading-[143%] font-normal text-[#212529] mb-0">Армения, Австрия, Азербайджан, Бельгия, Болгария, Кипр, Чешская Республика, Дания, Эстония,
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
	{name: 'Картой РФ', commission: '8%', imgUrl: new URL('../assets/visa-mastercard.png', import.meta.url).href},
	{name: 'Картой МИР', commission: '8%', imgUrl: new URL('../assets/visa-mastercard.png', import.meta.url).href},
	{name: 'СБП', commission: '8%', imgUrl: new URL('../assets/visa-mastercard.png', import.meta.url).href},
	{name: 'Payeer', commission: '8%', imgUrl: new URL('../assets/visa-mastercard.png', import.meta.url).href},
	{name: 'SteamPay', commission: '8%', imgUrl: new URL('../assets/visa-mastercard.png', import.meta.url).href},
	{name: 'Мегафон', commission: '8%', imgUrl: new URL('../assets/visa-mastercard.png', import.meta.url).href},
	{name: 'Билайн', commission: '8%', imgUrl: new URL('../assets/visa-mastercard.png', import.meta.url).href},
	{name: 'Tele2', commission: '8%', imgUrl: new URL('../assets/visa-mastercard.png', import.meta.url).href},
	{name: 'PayPal', commission: '8%', imgUrl: new URL('../assets/visa-mastercard.png', import.meta.url).href},
	{name: 'Stripe', commission: '8%', imgUrl: new URL('../assets/visa-mastercard.png', import.meta.url).href},
	{name: 'FKWallet', commission: '8%', imgUrl: new URL('../assets/visa-mastercard.png', import.meta.url).href},
	{name: 'Lava', commission: '8%', imgUrl: new URL('../assets/visa-mastercard.png', import.meta.url).href},
	{name: 'Volet', commission: '8%', imgUrl: new URL('../assets/visa-mastercard.png', import.meta.url).href},
	{name: 'PerfectMoney', commission: '8%', imgUrl: new URL('../assets/visa-mastercard.png', import.meta.url).href},
	{name: 'Другой', commission: '8%', imgUrl: new URL('../assets/visa-mastercard.png', import.meta.url).href},
	{name: 'FKWallet', commission: '8%', imgUrl: new URL('../assets/visa-mastercard.png', import.meta.url).href},
	{name: 'Lava', commission: '8%', imgUrl: new URL('../assets/visa-mastercard.png', import.meta.url).href},
	{name: 'Volet', commission: '8%', imgUrl: new URL('../assets/visa-mastercard.png', import.meta.url).href},
	{name: 'PerfectMoney', commission: '8%', imgUrl: new URL('../assets/visa-mastercard.png', import.meta.url).href},
	{name: 'Другой', commission: '8%', imgUrl: new URL('../assets/visa-mastercard.png', import.meta.url).href},
	{name: 'FKWallet', commission: '8%', imgUrl: new URL('../assets/visa-mastercard.png', import.meta.url).href},
	{name: 'Lava', commission: '8%', imgUrl: new URL('../assets/visa-mastercard.png', import.meta.url).href},
	{name: 'Volet', commission: '8%', imgUrl: new URL('../assets/visa-mastercard.png', import.meta.url).href},
	{name: 'PerfectMoney', commission: '8%', imgUrl: new URL('../assets/visa-mastercard.png', import.meta.url).href},
	{name: 'Другой', commission: '8%', imgUrl: new URL('../assets/visa-mastercard.png', import.meta.url).href},
]);

const showInfo = ref(false);
const toggleInfo = () => {
	showInfo.value = !showInfo.value;
};
</script>

<style scoped>
.payment-method:hover {
	border: 2px solid #E2C299;
}
</style>

