<template>
  <div class="min-h-screen bg-gray-100 p-6">
    <h1 class="text-3xl font-bold mb-6 text-center">Gestor de Tareas</h1>

    <!-- Entrada de nueva tarea -->
    <div class="flex justify-center gap-2 mb-6">
      <input
        v-model="nuevaTarea"
        @keyup.enter="agregarTarea"
        type="text"
        placeholder="Escribe el nombre de la tarea"
        class="border rounded-lg px-3 py-2 w-64 focus:outline-none focus:ring-2 focus:ring-blue-400"
      />
      <button
        @click="agregarTarea"
        class="bg-blue-500 hover:bg-blue-600 text-white px-4 py-2 rounded-lg"
      >
        Agregar
      </button>
    </div>

    <!-- Listado de tareas -->
    <div v-if="tareas.length === 0" class="text-center text-gray-500">
      No hay tareas registradas
    </div>

    <div v-else class="grid grid-cols-3 gap-4 mt-6">
      <!-- Columna To Do -->
      <div class="bg-blue-50 p-4 rounded-lg shadow">
        <h2 class="text-xl font-semibold text-blue-600 mb-3">To Do</h2>
        <div
          v-for="(tarea, index) in tareas.filter(t => t.estado === 'todo')"
          :key="index"
          class="bg-white border border-blue-300 p-2 rounded mb-2 flex justify-between items-center"
        >
          <span>{{ tarea.nombre }}</span>
          <button
            @click="moverTarea(tarea, 'doing')"
            class="text-green-500 hover:text-green-700"
          >
            ➡️
          </button>
        </div>
      </div>

      <!-- Columna Doing -->
      <div class="bg-green-50 p-4 rounded-lg shadow">
        <h2 class="text-xl font-semibold text-green-600 mb-3">Doing</h2>
        <div
          v-for="(tarea, index) in tareas.filter(t => t.estado === 'doing')"
          :key="index"
          class="bg-white border border-green-300 p-2 rounded mb-2 flex justify-between items-center"
        >
          <span>{{ tarea.nombre }}</span>
          <button
            @click="moverTarea(tarea, 'done')"
            class="text-red-500 hover:text-red-700"
          >
            ➡️
          </button>
        </div>
      </div>

      <!-- Columna Done -->
      <div class="bg-red-50 p-4 rounded-lg shadow">
        <h2 class="text-xl font-semibold text-red-600 mb-3">Done</h2>
        <div
          v-for="(tarea, index) in tareas.filter(t => t.estado === 'done')"
          :key="index"
          class="bg-white border border-red-300 p-2 rounded mb-2 flex justify-between items-center"
        >
          <span>{{ tarea.nombre }}</span>
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from "vue";

const nuevaTarea = ref("");
const tareas = ref([]);

// Agregar una nueva tarea
function agregarTarea() {
  if (nuevaTarea.value.trim() === "") return;
  tareas.value.push({ nombre: nuevaTarea.value, estado: "todo" });
  nuevaTarea.value = "";
}

// Cambiar el estado de una tarea
function moverTarea(tarea, nuevoEstado) {
  tarea.estado = nuevoEstado;
}
</script>

<style>
body {
  font-family: 'Inter', sans-serif;
}
</style>
