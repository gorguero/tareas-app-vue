<template>
  <div class="alert alert-warning mt-4 d-flex justify-content-around align-items-center">
    <p class="m-0" :class="{'tachado': tarea.estado}">{{tarea.texto}}</p>
    <div>
      <i class="fa-solid fa-rotate-left mx-2 text-success" role="button" @click="modificar(tarea.id)" v-if="tarea.estado"></i>
      <i class="fa-solid fa-circle-check mx-2 text-success" role="button" @click="modificar(tarea.id)" v-else></i>
      <i class="fa-solid fa-circle-minus mx-2 text-danger" role="button" @click="eliminar(tarea.id)"></i>
    </div>
  </div>
</template>

<script>
import { inject } from '@vue/runtime-core'
export default {

  props:{

    tarea:{
      type: Object,
      required: true
    }

  },

  setup(){

    const tareas = inject('tareas');

    const eliminar = id => tareas.value = tareas.value.filter(item => item.id !== id);

    const modificar = id => {

      tareas.value = tareas.value.map(item => {

        if(item.id === id){
          item.estado = !item.estado;
        }
        return item;
      });

    }

    return {eliminar, modificar}

  }

}
</script>

<style scoped>

  .tachado{
    text-decoration: line-through;
  }

</style>