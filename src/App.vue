<script setup>
  import Header from './components/Header.vue'

  /* Si utilizamos Options API agregamos lo siguiente y quitamos setup de etiqueta script*/
  // export default {
  //   components: {
  //     Header
  //   }
  // }
  function handleChange(e) {
    console.log(e.target.value);
  }
</script>

<template>
  <div class="my-20 max-w-lg mx-auto bg-white shadow p-10">
    <Header />

    <div class="my-5">
      <input 
        type="range"
        class="w-full bg-gray-200 accent-lime-500 hover:accent-lime-600"
        @input="handleChange"
      >
    </div>
  </div>
  
</template>

