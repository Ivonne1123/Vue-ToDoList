
<template>
  <div>
    <table class="table">
      <thead>
        <tr>
          <th>Index</th>
          <th>Check</th>
          <th scope="col">Title</th>
          <th scope="col">Description</th>
          <th scope="col">edit</th>
          <th scope="col">remove</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="(tarea, index) in todoItems" :key="index">
          <td>{{ index + 1 }}</td>
          <td> <input class="form-check-input" type="checkbox" id="flexCheckIndeterminate" v-model="tarea.done">
          </td>

          <!-- Si la tarea no se edita, permancen los datos  -->
          <td v-if="!tarea.editando">{{ tarea.title }}</td>
          <!-- pero si se edita, abre el input para cambiar los datos -->
          <td v-else>
            <input type="text" class="form-control" v-model.trim="tarea.title">
          </td>

          <!-- Si la tarea no se edita, permancen los datos  -->
          <td v-if="!tarea.editando">{{ tarea.description }}</td>
          <!-- pero si se edita, abre el input para cambiar los datos -->
          <td v-else>
            <input type="text" class="form-control" v-model.trim="tarea.description">
          </td>

          <!-- Si lqa tarea no se esta ditando, permanece el icono de "Editar" -->
          <td v-if="!tarea.editando">
            <svg @click="editarTarea(tarea)" xmlns="http://www.w3.org/2000/svg" width="25" height="25" fill="#9554AA"
              class="bi bi-pencil-square" viewBox="0 0 16 16">
              <path
                d="M15.502 1.94a.5.5 0 0 1 0 .706L14.459 3.69l-2-2L13.502.646a.5.5 0 0 1 .707 0l1.293 1.293zm-1.75 2.456-2-2L4.939 9.21a.5.5 0 0 0-.121.196l-.805 2.414a.25.25 0 0 0 .316.316l2.414-.805a.5.5 0 0 0 .196-.12l6.813-6.814z" />
              <path fill-rule="evenodd"
                d="M1 13.5A1.5 1.5 0 0 0 2.5 15h11a1.5 1.5 0 0 0 1.5-1.5v-6a.5.5 0 0 0-1 0v6a.5.5 0 0 1-.5.5h-11a.5.5 0 0 1-.5-.5v-11a.5.5 0 0 1 .5-.5H9a.5.5 0 0 0 0-1H2.5A1.5 1.5 0 0 0 1 2.5z" />
            </svg>
          </td>
          <!-- Pero si se edita la tarea, el icono "Editar" cambia a la palomita para posterior guardar los cambios -->
          <td v-else>
            <svg @click="guardarCambios(tarea)" xmlns="http://www.w3.org/2000/svg" width="25" height="25" fill="#9554AA"
              class="bi bi-check2-circle" viewBox="0 0 16 16">
              <path
                d="M2.5 8a5.5 5.5 0 0 1 8.25-4.764.5.5 0 0 0 .5-.866A6.5 6.5 0 1 0 14.5 8a.5.5 0 0 0-1 0 5.5 5.5 0 1 1-11 0" />
              <path
                d="M15.354 3.354a.5.5 0 0 0-.708-.708L8 9.293 5.354 6.646a.5.5 0 1 0-.708.708l3 3a.5.5 0 0 0 .708 0l7-7z" />
            </svg>
          </td>


          <td @click="eliminarTarea(index)">
            <svg xmlns="http://www.w3.org/2000/svg" width="25" height="25" fill="#9554AA" class="bi bi-trash-fill"
              viewBox="0 0 16 16">
              <path
                d="M2.5 1a1 1 0 0 0-1 1v1a1 1 0 0 0 1 1H3v9a2 2 0 0 0 2 2h6a2 2 0 0 0 2-2V4h.5a1 1 0 0 0 1-1V2a1 1 0 0 0-1-1H10a1 1 0 0 0-1-1H7a1 1 0 0 0-1 1zm3 4a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 .5-.5M8 5a.5.5 0 0 1 .5.5v7a.5.5 0 0 1-1 0v-7A.5.5 0 0 1 8 5m3 .5v7a.5.5 0 0 1-1 0v-7a.5.5 0 0 1 1 0" />
            </svg>
          </td>
        </tr>

      </tbody>
    </table>

  </div>
</template>

<script setup>
import { defineProps } from 'vue';

//las funciones las mando llamar como props para asignarlas en el template
const props = defineProps(['todoItems', 'eliminarTarea', 'editarTarea', 'guardarCambios'])
</script>