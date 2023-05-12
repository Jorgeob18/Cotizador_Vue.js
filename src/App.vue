<script setup>
import { ref, reactive, computed } from 'vue'
  import Header from './components/Header.vue'

  /* Si utilizamos Options API agregamos lo siguiente y quitamos setup de etiqueta script*/
  // export default {
  //   components: {
  //     Header
  //   }
  // }
  const cantidad = ref(10000);
  const MIN = 0;
  const MAX = 20000;
  const STEP = 100;

  // Compute Properties    
  const formatearDinero = computed(() => {
    const formatter = new Intl.NumberFormat('es-MX', {
      style: 'currency',
      currency: 'MXN'
    });
    return formatter.format(cantidad.value)
  })

  // const state = reactive({
  //   cantidad: 0
  // })
    
  // function handleChange(e) {
  //  cantidad.value = +e.target.value;
  // //  state.cantidad = Number(e.target.value)
  // }

  console.log(cantidad.value);
  // console.log(state.cantidad);
</script>

<template>
  <div class="my-20 max-w-lg mx-auto bg-white shadow p-10">
    <Header />
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
      <p class="text-center my-10 text-5xl font font-extrabold text-indigo-600"> {{formatearDinero}}</p>
      <!-- <p v-text="`$ ${cantidad}`"></p> -->
      <!-- <p v-html="`$ ${cantidad}`"></p> -->
    </div>
  </div>
  
</template>

