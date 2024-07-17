<template>
	<div class="mb-4">
		<h2 class="text-lg font-semibold mb-2">Выберите способ оплаты</h2>
		<div class="grid grid-cols-5 gap-[12px] mb-4 max-h-[242px] min-h-[100px] w-[100%] overflow-y-auto">
			<div
					v-for="method in methods"
					:key="method.title"
					class="payment-method flex items-center p-4 w-[219px] h-[68px] rounded-lg cursor-pointer"
					:class="{'hover:border-2 hover:border-[#E2C299]': selectedMethod?.title !== method.title, 'border-2 border-[#E2C299]': selectedMethod?.title === method.title}"
					@click="selectMethod(method)"
			>
				<div class="flex items-center">
					<img :src="importIcons[method.title]" width="15px" height="15px" :alt="method.title" class="w-6 h-6 mr-2">
					<div class="ml-3">
						<div class="font-semibold">{{ method.title }}</div>
						<div class="text-gray-500">Комиссия: {{ method.commission }}</div>
					</div>
				</div>
			</div>
		</div>
		<div @click="toggleInfo" class="flex w-[469px] mb-2 cursor-pointer items-center">
			<img src="../assets/warning-icon.svg" alt="warning-icon">
			<p class="text-[14px] font-medium text-[#212529] mb-0 mx-1">Внимание, при нажатии раскрывается информация
				про страны</p>
			<img :class="{'rotate-180': showInfo, 'rotate-0': !showInfo}" class="transition-transform duration-300 ml-1"
			     src="../assets/arrow-icon.svg" alt="arrow-icon">
		</div>
		<div v-if="showInfo" class="payments-info bg-gray-100 p-2 rounded">
			<p class="text-[14px] leading-[143%] font-normal text-[#212529] mb-0"
			   v-html="selectedMethodDescription"></p>
		</div>
	</div>
</template>

<script setup>
import {ref, watch} from 'vue';

const props = defineProps({
	methods: Array,
	modelValue: Object
});

const emit = defineEmits(['update:modelValue']);

const showInfo = ref(false);
const selectedMethodDescription = ref('');
const selectedMethod = ref(props.modelValue);

watch(() => props.modelValue, (newValue) => {
	selectedMethod.value = newValue;
	selectedMethodDescription.value = newValue ? newValue.description : 'Нет данных';
});

const toggleInfo = () => {
	showInfo.value = !showInfo.value;
};

const importIcons = {
	'Cryptomus': new URL('../assets/cryptomus.svg', import.meta.url).href,
	'Картой РФ': new URL('../assets/visa-mastercard.png', import.meta.url).href,
	'Payeer': new URL('../assets/payyer-icon.svg', import.meta.url).href,
	'Картой': new URL('../assets/mir-icon.svg', import.meta.url).href,
	'PayPal': new URL('../assets/paypal-icon.png', import.meta.url).href,
};

const selectMethod = (method) => {
	emit('update:modelValue', method);
	selectedMethod.value = method;
	selectedMethodDescription.value = method.description || "Нет данных";
};
</script>

<style scoped>
.payment-method:hover {
	border: 2px solid #E2C299;
}

.border-2 {
	border: 2px solid #E2C299;
}

.rotate-180 {
	transform: rotate(180deg);
}
</style>





