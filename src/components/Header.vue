<script setup>
import { computed } from 'vue'
import { RouterLink, useRoute } from 'vue-router'
import { useBebidasStore } from '../stores/bebidas'
import { useNotificacionStore } from '../stores/notificaciones'
const route = useRoute()
const store = useBebidasStore()
const notificacion = useNotificacionStore()
const paginaInicio = computed(() => route.name === 'inicio')
const handleSubmit = () => {
  if (Object.values(store.busqueda).includes('')) {
    notificacion.$patch({
      texto: 'Todos los campos son obligatorios',
      mostrar: true,
      error: true
    })
    return
  }
  store.obtenerRecetas()
}
</script>

<template>
  <header class="bg-slate-800" :class="{ header: paginaInicio }">
    <div class="mx-auto container px-5 py-16">
      <div class="flex justify-between items-center">
        <div class="">
          <RouterLink :to="{ name: 'inicio' }">
            <img src="/img/logo.svg" class="w-32" alt="Logotipo" />
          </RouterLink>
        </div>
        <nav class="flex gap-4 text-white"
          ><RouterLink
            :to="{ name: 'inicio' }"
            class="font-bold uppercase"
            active-class="text-orange-400"
            >Inicio</RouterLink
          >
          <RouterLink
            :to="{ name: 'favoritos' }"
            class="font-bold uppercase"
            active-class="text-orange-400"
            >Favoritos</RouterLink
          >
        </nav>
      </div>
      <form
        class="md:w-1/2 2xl:w-1/3 bg-orange-400 my-32 rounded-lg p-10 shadow space-y-6"
        v-if="paginaInicio"
        @submit.prevent="handleSubmit">
        <div class="space-y-4">
          <label
            class="block text-white font-extrabold uppercase text-lg"
            for="ingrediente"
            >Nombre o Ingredientes</label
          >
          <input
            type="text"
            id="ingrediente"
            class="p-3 w-full rounded-lg focus:out-of-range:"
            placeholder="Nombre o Ingrediente: Vodka, Tequila, etc"
            v-model="store.busqueda.nombre" />
        </div>
        <div class="space-y-4">
          <label
            class="block text-white font-extrabold uppercase text-lg"
            for="categoria"
            >Categoria</label
          >
          <select
            id="categoria"
            class="p-3 w-full rounded-lg focus:out-of-range:"
            v-model="store.busqueda.categoria">
            <option value="">-- Seleccione --</option>
            <option
              v-for="categoria in store.categorias"
              :key="categoria.strCategory"
              :value="categoria.strCategory"
              >{{ categoria.strCategory }}</option
            >
          </select>
        </div>
        <input
          type="submit"
          value="Buscar Recetas"
          class="bg-orange-800 hover:bg-orange-950 cursor-pointer text-white font-extrabold p-2 w-full rounded-lg uppercase" />
      </form>
    </div>
  </header>
</template>
<style>
.header {
  background-image: url('/img/bg.jpg');
  background-size: cover;
  background-position: center;
  background-repeat: no-repeat;
}
</style>
