<script setup>
import { ref, reactive } from 'vue'
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

  // const state = reactive({
  //   cantidad: 0
  // })
    
  function handleChange(e) {
   cantidad.value = +e.target.value;
  //  state.cantidad = Number(e.target.value)
  }

  console.log(cantidad.value);
  // console.log(state.cantidad);
</script>

<template>
  <div class="my-20 max-w-lg mx-auto bg-white shadow p-10">
    <Header />

    <div class="my-5">
      <input 
        type="range"
        class="w-full bg-gray-200 accent-lime-500 hover:accent-lime-600"
        min="0"
        max="20000"
        step="100"
        value="10000"
        @input="handleChange"
      />
      <!-- {{ cantidad }} -->
      <!-- {{ state.cantidad }} -->
      <p>$ {{cantidad}}</p>
      <!-- <p v-text="`$ ${cantidad}`"></p> -->
      <!-- <p v-html="`$ ${cantidad}`"></p> -->
    </div>
  </div>
  
</template>

