<template>
	<div class="container py-10 md:py-20 mx-auto">
		<h1 class="main-title font-bold text-3xl leading-tight text-gray-900 mb-8">
			Пополните баланс,
			<span class="subtitle font-medium text-gray-600">чтобы получить номер для приема смс</span>
		</h1>
		<CurrencySelector />
		<PaymentMethodSelector />
		<PaymentAmountInput />
		<button class="custom-button w-full h-16 rounded-lg px-5 font-medium text-white bg-gradient-to-r from-[#e2c299] to-[#c5a67c]">Оплатить</button>
	</div>
</template>

<script setup>
import CurrencySelector from './components/CurrencySelector.vue'
import PaymentMethodSelector from './components/PaymentMethodSelector.vue'
import PaymentAmountInput from './components/PaymentAmountInput.vue'
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

