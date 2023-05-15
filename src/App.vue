<script setup>
import { ref, reactive, computed } from 'vue'
  import Header from './components/Header.vue'
  import Button from './components/Button.vue'
  import { calcularTotalPagar, formatearDinero } from './helpers'

  /* Si utilizamos Options API agregamos lo siguiente y quitamos setup de etiqueta script*/
  // export default {
  //   components: {
  //     Header
  //   }
  // }
  const cantidad = ref(10000);
  const meses = ref(6);
  const total = ref(calcularTotalPagar(cantidad.value, meses.value))
  const MIN = 0;
  const MAX = 20000;
  const STEP = 100;

  // Compute Properties    
  // const formatearDinero = computed(() => {
  //   const formatter = new Intl.NumberFormat('es-MX', {
  //     style: 'currency',
  //     currency: 'MXN'
  //   });
  //   return formatter.format(cantidad.value)
  // });

  const handleChangeDecremento = () => {
    const valor = cantidad.value - STEP
    if (valor < MIN) {
      alert("Cantidad no valida");
      return;
    } 
    cantidad.value = valor
  }

  const handleChangeIncremento = () => {
    const valor = cantidad.value + STEP
    if (valor > MAX) {
      alert("Cantidad no valida");
      return;
    } 
    cantidad.value = valor
  }

  // const state = reactive({
  //   cantidad: 0
  // })
    
  // function handleChange(e) {
  //  cantidad.value = +e.target.value;
  // //  state.cantidad = Number(e.target.value)
  // }

  // console.log(state.cantidad);
</script>

<template>
  <div class="my-20 max-w-lg mx-auto bg-white shadow p-10">
    <Header />
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
    <!-- Agregtar atributos dinamicos con ":" antes del atributo, al hacer esto buscara el valor en la variable -->
    <div class="my-5">
      <input 
        type="range"
        class="w-full bg-gray-200 accent-lime-500 hover:accent-lime-600"
        :min="MIN"
        :max="MAX"
        :step="STEP"
        
        v-model.number="cantidad"
      />
      <!-- Con v-model para modificar el State no necesitamos especificar el atributo Value y el envento @input | adicionalmente agregamos el modificador "number" para convertir a numero" -->
      
      <!-- {{ cantidad }} -->
      <!-- {{ state.cantidad }} -->
      <p class="text-center my-10 text-5xl font font-extrabold text-indigo-600"> 
        {{formatearDinero(cantidad)}}
      </p>
      <!-- <p v-text="`$ ${cantidad}`"></p> -->
      <!-- <p v-html="`$ ${cantidad}`"></p> -->
      <h2 class="text-2xl font-extrabold text-gray-500 text-center">
        Elige un <span class="text-indigo-600">Plazo </span> a pagar.
      </h2>
      <select 
        class="w-full p-2 bg-white border border-gray-300 rounded-lg text-center text-xl font-bold text-gray-500 mt-5" 
        :value="meses"
        v-model.number="meses"
      >
        <option value="6">6 Meses</option>
        <option value="12">12 Meses</option>
        <option value="24">24 Meses</option>
      </select>
    </div>
    <div class="my-5 space-y-3-bg-gray-50 p-5">
      <h2 class="text-2xl font-extrabold text-gray-500 text-center">
        Resumen <span class="text-indigo-600">de pagos</span>
      </h2>
      <p class="text-xl text-gray-500 text-center font-bold">Meses: {{meses}}</p>
      <p class="text-xl text-gray-500 text-center font-bold">Total a pagar: {{formatearDinero(total)}}</p>
      <p class="text-xl text-gray-500 text-center font-bold">Mensuales:</p>
    </div>
  </div>
  
</template>

