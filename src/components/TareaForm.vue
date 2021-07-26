<template>
  <form @submit.prevent="agregarTarea">
      <input type="text" placeholder="Ingrese tarea" v-model.trim="tareaInput">
      <button class="btn btn-primary w-100">
          Agregar
      </button>
  </form>
</template>

<script>
import { inject, ref } from '@vue/runtime-core'
export default {
    setup(){
        const tareas = inject('tareas');
        const tareaInput = ref('');

        const agregarTarea = () => {
            if(tareaInput.value === '')return console.log('Texto vacío');

            const tarea = {
                texto: tareaInput.value,
                completada: false,
                id: Date.now()
            }

            tareas.value.push(tarea);
            tareaInput.value = '';
        }

        return { agregarTarea, tareaInput }
    }
}
</script>