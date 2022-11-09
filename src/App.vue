<script setup>
import { RouterLink, RouterView } from 'vue-router';
import { todosFactory } from './todosSetup';
import { ref } from 'vue';
import todoService from './services/todoServices';

const { update } = todosFactory();

const isLoading = ref(true);
async function prefetch() {
  update(await todoService.getTodos());
  isLoading.value = false;
}
prefetch();
</script>

<template>
  <div class="container">
    <h2 v-if="isLoading">Cargando Datos...</h2>
    <template v-if="!isLoading">
      <ul>
        <RouterLink to="/">
          <li>Lista Tareas</li>
        </RouterLink>
        <RouterLink to="/new">
          <li>Nueva Tarea</li>
        </RouterLink>
      </ul>
      <RouterView />
    </template>
  </div>
</template>

<style>
@import './assets/base.css';
</style>
