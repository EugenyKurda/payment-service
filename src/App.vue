<template>
	<div class="container py-10 md:py-20 mx-auto">
		<h1 class="main-title font-bold text-3xl leading-tight text-gray-900 mb-8">
			Пополните баланс,
			<span class="subtitle font-medium text-gray-600">чтобы получить номер для приема смс</span>
		</h1>
		<CurrencySelector :currencies="currencies" v-model="selectedCurrency" />
		<PaymentMethodSelector :methods="paymentMethods" v-model="selectedMethod" />
		<PaymentAmountInput :minAmount="minAmount" v-model="amount" />
		<button @click="handlePayment" class="custom-button w-full h-16 rounded-lg px-5 font-medium text-white bg-gradient-to-r from-[#e2c299] to-[#c5a67c]">Оплатить</button>
		<div v-if="errorMessage" class="text-red-500 mt-4">{{ errorMessage }}</div>
	</div>
</template>

<script setup>
import { ref, onMounted, computed, watch } from 'vue';
import CurrencySelector from './components/CurrencySelector.vue';
import PaymentMethodSelector from './components/PaymentMethodSelector.vue';
import PaymentAmountInput from './components/PaymentAmountInput.vue';
import axios from 'axios';

const currencies = ref({});
const paymentMethods = ref([]);
const selectedCurrency = ref('');
const selectedMethod = ref(null);
const amount = ref('');
const errorMessage = ref('');

const minAmount = computed(() => selectedMethod.value?.min_amount || 0);

onMounted(async () => {
	try {
		const response = await axios.get('/mockData.json');
		const data = response.data.data;
		currencies.value = data.currencies;
		selectedCurrency.value = data.default_currency;
		paymentMethods.value = data.currencies[selectedCurrency.value];

		console.log(currencies.value, 'currencies.value ')
		console.log(selectedCurrency.value, 'selectedCurrency.value')
		console.log(paymentMethods.value, 'paymentMethods.value')
	} catch (error) {
		console.error('Ошибка загрузки данных:', error);
	}
});

watch(selectedCurrency, (newCurrency) => {
	paymentMethods.value = currencies.value[newCurrency];
	selectedMethod.value = null;
});

const handlePayment = async () => {
	if (parseInt(amount.value) < minAmount.value) {
		errorMessage.value = `Минимальная сумма для ${selectedMethod.value.title}: ${minAmount.value}₽`;
		return;
	}

	try {
		console.log('Payment processed', {
			currency: selectedCurrency.value,
			method: selectedMethod.value.title,
			amount: parseInt(amount.value),
		});
		// Пример POST-запроса для оплаты
		// const response = await axios.post('/api/ui/payment/pay', {
		//   currency: selectedCurrency.value,
		//   method: selectedMethod.value.title,
		//   amount: parseInt(amount.value),
		// });
		// const paymentUrl = response.data.payment_url;
		// window.location.href = paymentUrl;
	} catch (error) {
		errorMessage.value = 'Ошибка при обработке платежа: ' + error.message;
	}
};
</script>

<style scoped>
.container {
	padding: 40px 0 80px 0;
	margin: 0 auto;
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

.custom-button {
	width: 100%;
	height: 4rem;
	border-radius: 0.5rem;
	padding: 0 1.25rem;
	font-weight: 500;
	color: #fff;
	background: linear-gradient(to right, #e2c299, #c5a67c);
}
</style>


