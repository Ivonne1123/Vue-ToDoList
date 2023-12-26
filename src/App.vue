<template>
  <div class="container">

    <Header :tareas-completadas="tareasCompletadas" :total-tareas="totalTareas"
      :porcentaje-completado="porcentajeCompletado" />

    <!-- FORMULARIO DE REGISTRO DE TAREAS -->
    <TodoList :registroTarea="agregarNuevaTarea" />

    <!-- TABLA DE TAREAS -->
    <TodoListItems :todoItems="todoItems" :editarTarea="editarTarea" :eliminarTarea="eliminarTarea"
      :guardarCambios="guardarCambios" :index="index"/>

  </div>
</template>

<script setup>
import { ref, computed, defineProps, defineEmits } from 'vue';
//importa los componentes 
import Header from './components/Header.vue';
import TodoList from './components/TodoList.vue';
import TodoListItems from './components/TodoListItem.vue'

//llamo los eventos como props
const props = defineProps(['title', 'description','nuevaTarea', 'index', ]);

//emite el evento Registro tarea deade todolist que funciona
const emit=defineEmits(['registroTarea'])

//aaray donde se guardaran todas las tareas
const todoItems = ref([]);


function agregarNuevaTarea(nuevaTarea){
  //ingresa los registros de las nuevas tareas a tidoitems
  todoItems.value.push({
    ...nuevaTarea,
    //mantiene el input cerrado , solo se abre en caso de editar la tarea
    editando: false, 
  });

   //llama al avento registro tarea y pasa el objeto de nueva tarea para limpiar los campos del formulario.
emit('registroTarea', nuevaTarea);



};

//abre el input para editar la tarea.
function editarTarea(tarea) {
  tarea.editando = true;
};

function guardarCambios(tarea) {
  //const datosOriginales = { ...tarea };
    const resultado = window.confirm('¿Estás seguro de guardar los cambios?');
    //si resultado es true, me arroja el mensaje de actualizar tarea y cierra el input con los nuevos datos
  if (resultado === true) {
    alert('Tarea Actualizada')
    tarea.editando = false;
  } else {
    //datosOriginales
    //cierra el input
    tarea.editando = false;
  };
};

//elimina tarea funciona para el Index
function eliminarTarea(index) {
  const resultado = window.confirm('¿Estás seguro de eliminar la tarea?');
  if (resultado) {
    //actualiza el todoitems en caso de dar en aceptar a la confirmacion
    todoItems.value.splice(index, 1);
    //si cancenlas la peticion, no borra nada.
  };
};

//calcula el total de las tareas obteniendo el tamano del array todoItems
const totalTareas = computed(() => todoItems.value.length);
//me filtra unicamente los valores de "done" en su valor true
const tareasCompletadas = computed(() => todoItems.value.filter(item => item.done).length);
const porcentajeCompletado = computed(() => (tareasCompletadas.value / totalTareas.value) * 100 || 0);

</script>
