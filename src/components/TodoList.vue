<template>
  <div class="mt-4">
    <form @submit.prevent="TareaRegistrada">
      <div class="row">
        <div class="col-4 mb-3">
          <input type="text" class="form-control" placeholder="Title" v-model.trim="title" required>
        </div>
        <div class="col-7 mb-3">
          <input type="text" class="form-control" placeholder="Description" v-model.trim="description" required>
        </div>
        <div class="col mb-4">
          <button type="submit" class="btn" style="background-color: #9554AA; color: white; font-weight: 500;">Add</button>
        </div>
      </div>
    </form>
  </div>
</template>

<script setup>
import { ref, defineProps } from 'vue';

//extrae todas las propiedad registroTarea y lo define como un prop
const { registroTarea } = defineProps(['registroTarea']);

//porpiedades reactivas
const title = ref("");
const description = ref("");

function TareaRegistrada() {
  //crea un obj  nuevatarea donde se asignan los valores de title y description que se ingresan desde el formulario
  const nuevaTarea = {
    title: title.value,
    description: description.value,
    //el atributo se vera reflejado en el check cuando la tarea este registrada
    done: false,
  };
  
  // registroTarea pasa el objeto nuevaTarea como argumento.
  registroTarea(nuevaTarea);
  title.value = "";
  description.value = "";
}
 

</script>
