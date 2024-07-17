<template>
	<div class="mb-4">
		<div class="flex items-center mb-4">
			<h2 class="text-xl text-gray-900 mr-2">Выберите валюту оплаты</h2>
			<div class="relative inline-block group">
				<img src="../assets/question-icon.svg" class="transition-all duration-300 hover:bg-black hover:rounded-full hover:invert" alt="question-icon">
				<div class="hidden absolute top-5 right-[-360px] transform -translate-x-1/2 text-start shadow-lg bg-white z-10 rounded-xl p-2 w-[247px] h-[56px] group-hover:block">
					<p class="font-medium text-[14px] text-gray-900 leading-5">Тут выбирается способ которым вы будете оплачивать</p>
				</div>
			</div>
		</div>
		<div class="flex gap-4">
			<div
					class="flex items-center justify-between rounded-lg p-4 w-fit h-[68px] shadow-sm bg-white cursor-pointer"
					@click="selectCurrency('CRYPTO')"
			>
				<img :src="iconPaths['CRYPTO']" alt="btc" class="w-6 h-6 mr-2">
				<span>Криптовалюты</span>
			</div>
			<div
					class="flex items-center justify-between rounded-lg p-4 w-fit h-[68px] shadow-sm bg-white cursor-pointer hover:border-[#e2c299]"
					@click="toggleCurrencies"
			>
				<div class="flex items-center border-r border-gray-200 pr-4">
					<img :src="iconPaths[selectedCurrency]" alt="RUB" class="w-6 h-6 mr-2">
					<span>{{ selectedCurrency|| 'RUB' }}</span>
				</div>
				<div class="flex items-center cursor-pointer ml-[10px]">
					<img src="../assets/exchange.svg" alt="exchange" class="w-6 h-6">
					<span class="ml-2">Другие валюты</span>
					<img :class="{'rotate-180': showCurrencies, 'ml-2': true}" src="../assets/arrow-icon.svg" alt="arrow-icon">
				</div>
			</div>
		</div>
		<div v-if="showCurrencies" class="grid grid-cols-9 gap-3 mb-4 overflow-auto max-h-[131px]">
			<div
					v-for="(currency, key) in currencies"
					:key="key"
					@click="selectCurrency(key)"
					:class="['flex items-center rounded-lg p-4 min-w-[115px] max-w-[220px] h-[58px] cursor-pointer hover:border-2 hover:border-[#E2C299]', {'border-2 border-[#E2C299]': selectedCurrency === key}]"
			>
				<img :src="iconPaths[key]" :alt="key" class="w-7 h-6 mr-2">
				<span class="max-w-fit">{{ key }}</span>
			</div>
		</div>
	</div>
</template>

<script setup>
import { ref, watch, defineProps, defineEmits } from 'vue';

// Dynamically import icons
const importIcons = () => {
	return {
		CRYPTO: new URL('../assets/btc.svg', import.meta.url).href,
		RUB: new URL('../assets/rub-icon.svg', import.meta.url).href,
		USD: new URL('../assets/usd-icon.svg', import.meta.url).href,
		Cryptomus: new URL('../assets/cryptomus.svg', import.meta.url).href,
	};
};

const props = defineProps({
	currencies: {
		type: Object,
		required: true
	},
	modelValue: {
		type: String,
		required: true
	}
});

const emit = defineEmits(['update:modelValue']);

const showCurrencies = ref(false);
const selectedCurrency = ref(props.modelValue);
const iconPaths = ref(importIcons());

const toggleCurrencies = () => {
	showCurrencies.value = !showCurrencies.value;
};

const selectCurrency = (currencyKey) => {
	selectedCurrency.value = currencyKey;
	emit('update:modelValue', currencyKey);
	showCurrencies.value = false;
};

watch(() => props.modelValue, (newValue) => {
	selectedCurrency.value = newValue;
});
</script>

<style scoped>
/* Скрытие элемента по умолчанию */
.group-hover\:block {
	display: none;
}

/* Показ элемента при наведении на родителя */
.group:hover .group-hover\:block {
	display: block;
}

/* Вращение иконки при раскрытии списка валют */
.rotate-180 {
	transform: rotate(180deg);
}
</style>






