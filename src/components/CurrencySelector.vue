<template>
	<div class="mb-4">
		<div class="flex items-center mb-4">
			<h2 class="text-xl text-gray-900 mr-2">Выберите валюту оплаты</h2>
			<div class="relative inline-block">
				<img src="../assets/question-icon.svg" class="transition-all duration-300 hover:bg-black hover:rounded-full hover:invert" alt="question-icon">
				<div class="hidden absolute top-5 right-[-360px] transform -translate-x-1/2 text-start shadow-lg bg-white z-10 rounded-xl p-3 w-[247px] h-[56px] group-hover:block">
					<p class="font-medium text-sm text-gray-900 leading-6">Тут выбирается способ которым вы будете оплачивать</p>
				</div>
			</div>
		</div>
		<div class="flex gap-4">
			<div class="flex items-center justify-between rounded-lg p-4 w-fit h-[68px] shadow-sm bg-white cursor-pointer hover:border-[#e2c299]">
				<img src="../assets/btc.svg" alt="btc" class="w-6 h-6 mr-2">
				<span>Криптовалюты</span>
			</div>
			<div class="flex items-center justify-between rounded-lg p-4 w-fit h-[68px] shadow-sm bg-white cursor-pointer hover:border-[#e2c299]">
				<div class="flex items-center border-r border-gray-200 pr-4">
					<img src="../assets/rub-icon.svg" alt="RUB" class="w-6 h-6 mr-2">
					<span>RUB</span>
				</div>
				<div class="flex items-center cursor-pointer" @click="toggleCurrencies">
					<img src="../assets/exchange.svg" alt="exchange" class="w-6 h-6">
					<span class="ml-2">Другие валюты</span>
					<img :class="{'rotate-180': showCurrencies, 'ml-2': true}" src="../assets/arrow-icon.svg" alt="arrow-icon">
				</div>
			</div>
		</div>
		<div v-if="showCurrencies" class="grid grid-cols-9 gap-3 mb-4 overflow-auto max-h-[131px]">
			<div class="flex items-center rounded-lg p-4 w-[111px] h-[58px] cursor-pointer hover:border-2 hover:border-[#E2C299]" v-for="method in 10" :key="method">
				<img src="../assets/rub-icon.svg" alt="RUB" class="w-6 h-6 mr-2">
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
/* Скрытие элемента по умолчанию */
.group-hover\:block {
	display: none;
}

/* Показ элемента при наведении на родителя */
.group:hover .group-hover\:block {
	display: block;
}
</style>



