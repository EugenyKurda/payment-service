<template>
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
		<div class="button-group">
			<button v-for="amount in amounts" :key="amount" class="amount-button">
				{{ amount }}
			</button>
		</div>
	</div>
</template>

<script setup>
import { ref, watch } from 'vue';

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

const amounts = ref(['1.000₽', '2.000₽', '5.000₽', '10.000₽', '20.000₽', '50.000₽']);
</script>

<style scoped>
@import '../style.css';

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

.button-group {
	display: flex;
	gap: 8px;
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
