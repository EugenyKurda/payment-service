<template>
	<div>
		<h2 class="text-lg font-semibold mb-2">Укажите сумму платежа</h2>
		<div>
			<div class="input-group">
				<input
						type="text"
						:placeholder="`Минимальная сумма платежа: ${minAmount}${currencySymbol}`"
						class="payment-input"
						:class="{'active': isActive, 'error': hasError}"
						:value="displayValue"
						@focus="isActive = true"
						@blur="handleBlur"
						@input="handleInput"
						@keydown="handleKeyDown"
						ref="amountInput"
				/>
				<button v-if="inputValue" @click="clearInput" class="clear-button">✕</button>
			</div>
			<div v-if="hasError" class="error-message mb-[15px]">
				Внимание, минимальная сумма {{ minAmount }}{{ currencySymbol }}
			</div>
		</div>
		<div class="button-group">
			<button v-for="amount in amounts" :key="amount" class="amount-button" @click="selectAmount(amount)">
				{{ amount }}{{ currencySymbol }}
			</button>
		</div>
	</div>
</template>

<script setup>
import {ref, watch, onMounted, nextTick} from 'vue';

const props = defineProps({
	minAmount: Number,
	modelValue: String,
	currency: String
});

const emit = defineEmits(['update:modelValue']);

const isActive = ref(false);
const hasError = ref(false);
const inputValue = ref(props.modelValue);
const displayValue = ref('');

const currencySymbol = ref('₽');

const updateCurrencySymbol = (currency) => {
	switch (currency) {
		case 'USD':
			currencySymbol.value = '$';
			break;
		case 'EUR':
			currencySymbol.value = '€';
			break;
		case 'RUB':
			currencySymbol.value = '₽';
			break;
		case 'CRYPTO':
			currencySymbol.value = '₿';
			break;
		default:
			currencySymbol.value = '₽';
	}
	updateDisplayValue();
};

const updateDisplayValue = () => {
	displayValue.value = inputValue.value ? `${inputValue.value}${currencySymbol.value}` : '';
};

watch(() => props.currency, (newCurrency) => {
	updateCurrencySymbol(newCurrency);
});

watch(inputValue, (newValue) => {
	emit('update:modelValue', newValue);
	validateInput();
	updateDisplayValue();
});

onMounted(() => {
	updateCurrencySymbol(props.currency);
	updateDisplayValue();
});

const clearInput = () => {
	inputValue.value = '';
	hasError.value = false;
	updateDisplayValue();
};

const handleBlur = () => {
	isActive.value = false;
	validateInput();
};

const handleInput = (event) => {
	nextTick(() => {
		const input = event.target;
		input.selectionStart = input.selectionEnd = input.value.length - 1; // Move the cursor before the currency symbol
	});
	let value = event.target.value.replace(/[^\d]/g, ''); // Remove all non-digit characters
	inputValue.value = value ? `${parseInt(value).toLocaleString()}` : '';
	updateDisplayValue();

	nextTick(() => {
		const input = event.target;
		input.selectionStart = input.selectionEnd = input.value.length - 1; // Move the cursor before the currency symbol
	});
};

const handleKeyDown = (event) => {
	const input = event.target;
	const cursorPosition = input.selectionStart;

	// Prevent moving cursor beyond the numeric value
	if ((event.key === 'ArrowRight' && cursorPosition >= input.value.length - 1) || (event.key === 'ArrowLeft' && cursorPosition <= 0)) {
		event.preventDefault();
	}
};

const validateInput = () => {
	const numericValue = parseInt(inputValue.value.replace(/[^\d]/g, '')); // Extract numeric value
	hasError.value = numericValue < props.minAmount;
};

const amounts = ref(['1.000', '2.000', '5.000', '10.000', '20.000', '50.000']);

const selectAmount = (amount) => {
	inputValue.value = amount.replace(/[^\d]/g, '');
	hasError.value = parseInt(amount.replace(/[^\d]/g, '')) < props.minAmount;
	updateDisplayValue();
};
</script>

<style scoped>
.input-group {
	position: relative;
	display: flex;
	align-items: center;
	margin-bottom: 10px;
}

.payment-input {
	width: 100%;
	padding: 8px 12px;/* добавляем отступ для значка валюты */
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

.payment-input:focus-visible {
	outline: none;
	border: 2px solid #E2C299;
}

.currency-symbol {
	position: absolute;
	right: 10px;
	font-size: 14px;
	color: rgba(33, 37, 41, 0.6);
}

.clear-button {
	position: absolute;
	right: 35px;
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

.button-group {
	display: flex;
	gap: 8px;
	margin-bottom: 30px;
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
	border: none;
	cursor: pointer;
	display: flex;
	align-items: center;
	justify-content: center;
}

.amount-button:hover {
	border: 2px solid #E2C299;
}
</style>


