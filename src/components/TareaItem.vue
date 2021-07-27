<template>
    <div class="alert alert-warning mt-3 d-flex justify-content-between align-items-center">
        <p class="m-0" :class="{'tachado': tarea.completada}">{{ tarea.texto }}</p>
        <div>
            <i class="fas fa-undo-alt mx-2 text-success" 
            role="button"
            @click="modificarTarea(tarea.id)"
            v-if="tarea.completada"
            ></i>
            <i class="fas fa-check-circle mx-2 text-success" 
            role="button"
            @click="modificarTarea(tarea.id)"
            v-else
            ></i>
            <i class="fas fa-minus-circle text-danger" role="button"
                @click="eliminarTarea(tarea.id)"
            ></i>
        </div>
    </div>
</template>

<script>
import { inject } from '@vue/runtime-core';
export default {
    props: {
        tarea: Object
    },
    setup(){
        const tareas = inject('tareas');
        
        const eliminarTarea = id => {
            tareas.value = tareas.value.filter(item => item.id !== id);
        }

        const modificarTarea = (id) => {
            tareas.value = tareas.value.map(item => {

                if(item.id === id){
                    item.completada = !item.completada
                }

                return item;
            })
        }

        return { eliminarTarea, modificarTarea }
    }
}
</script>

<style scoped>
    .tachado{
        text-decoration: line-through;
    }
</style>