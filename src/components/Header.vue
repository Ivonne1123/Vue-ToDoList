<template>
<!-- BARRA DE PROGRESO -->
  <!-- Me concatena el valor de las tareas completadas / el total de las tareas -->
  <div class="row">
    <div class="col-6 mt-4">
      <div class="container">
<nav class="navbar fw-semibold" >
  <div class="container-flex">
    <a class="navbar-brand">
      <img src="https://www.pngitem.com/pimgs/m/80-802858_icon-check-list-png-transparent-png.png" alt="Logo" width="40" height="40" class="d-inline-block align-text-top">
      To Do List
    </a>
  </div>
</nav>
</div>
    </div>
    <div class="col-6 mt-4">
      <h4 class="text-end"> {{ tareasCompletadas }}/{{ totalTareas }}</h4>
      <div class="progress">
        <div class="progress-bar progress-bar-striped progress-bar-animated" role="progressbar"
          :aria-valuenow="porcentajeCompletado" aria-valuemin="0" aria-valuemax="100"
          :style="{ width: porcentajeCompletado + '%', backgroundColor: '#9554AA' }"></div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { defineProps } from 'vue';
//Los props vienen de fuera y los mando llamar desde el todolist, el evento viene desde el app.vue
const props = defineProps(['tareasCompletadas', 'totalTareas', 'porcentajeCompletado']);


</script>