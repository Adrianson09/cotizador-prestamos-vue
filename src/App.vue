<script setup>
import {ref, computed} from 'vue';
import Header from './components/Header.vue';
import Button from './components/Button.vue';
import {totalPagar} from './helpers/index.js'

const cantidad = ref(100000);
const meses = ref(6);
const total = ref(totalPagar(cantidad.value, meses.value));
const MIN= 0;
const MAX= 200000;
const STEP= 5000;

const formatearDinero = computed(() => {
  const formatter = new Intl.NumberFormat('es-CR',{
    style: 'currency',
    currency: 'CRC'
  });
  return formatter.format(cantidad.value)
});

const handleChangeDecremento = () => {
  if (cantidad.value > MIN) {
    cantidad.value = cantidad.value - STEP;
  }
  
}
const handleChangeIncremento = () => {
  if (cantidad.value < MAX) {
    cantidad.value = cantidad.value + STEP;
  }
  
}

</script>

<template>
  <div class="my-20 max-w-lg mx-auto bg-white shadow p-10">
      <Header/>

      <div class="flex justify-between mt-10">
        <Button
        :operador="'-'"
        @fn="handleChangeDecremento"
        />
        <Button
        :operador="'+'"
        @fn="handleChangeIncremento"
        />
       

      </div>
      <div class="my-5">
        <input 
        type="range"
        class="w-full bg-gray-200 accent-lime-500 hover:accent-lime-600"
        :min="MIN"
        :max="MAX"
        :step="STEP"
        v-model.number="cantidad"
       
        />
        <p class="text-center my-10 text-5xl font-extrabold text-green-800">{{ formatearDinero }}</p>
        <h2 class="text-2xl font-extrabold text-gray-500 text-center">
          Elige un <span class="text-green-800">Plazo</span> a Pagar
        </h2>

        <select class="w-full p-2 bg-white border border-gray-300 rounded-lg text-center
        text-xl font-bold text-gray-500 mt-5"
        :value="meses"
        v-model.number="meses">
          <option value="6">6 Meses</option>
          <option value="12">12 Meses</option>
          <option value="24">24 Meses</option>
        </select>
      </div>
      <div class="my-5 space-y-3 bg-gray-50 p-5">
        <h2 class="text-2xl font-extrabold text-gray-500 text-center">
          Resumen <span class="text-green-800">de Pagos</span>
        </h2>
        <p class="text-xl text-gray-500 text-center font-bold">{{ meses }} Meses</p>
        <p class="text-xl text-gray-500 text-center font-bold">Total a pagar: {{ formatearDinero( total ) }}</p>
        <p class="text-xl text-gray-500 text-center font-bold">Mensualidades de: </p>

      </div>
  </div>
 
</template>

<style scoped>

</style>
