<script setup>
import { useBebidasStore } from '../stores/bebidas';
const bebida = useBebidasStore()
defineProps({
  receta: {
    type: Object,
    required: true
  }
})
</script>

<template>
  <div class="border shadow-lg">
    <div class="overflow-hidden">
      <img
        :src="receta.strDrinkThumb"
        :alt="'magen de ' + receta.strDrink"
        class="hover:scale-125 transition-transform hover:rotate-2" />
    </div>
    <div class="p-5">
      <h2 class="text-2xl truncate font-extrabold">{{ receta.strDrink }}</h2>
      <button
        class="bg-orange-400 mt-5 w-full p-3 font-bold text-white text-lg hover:bg-orange-500"
        type="button" @click="bebida.seleccionarBebida(receta.idDrink)"
        >Ver Receta</button
      >
    </div>
  </div>
</template>
