<template>
    <h1>App Tareas</h1>
    <tarea-form />
    <tarea-item 
        v-for="tarea in tareas"
        :key="tarea.id"
        :tarea="tarea"
    />
    <div class="alert alert-dark mt-3" v-if="tareas.length === 0">
        Sin tareas pendientes 😄
    </div>
    {{ tareas }}
</template>
<script>
import { ref } from '@vue/reactivity'
import TareaForm from './TareaForm.vue';
import { provide } from '@vue/runtime-core';
import TareaItem from './TareaItem.vue';

export default {
  components: { TareaForm, TareaItem },
    setup(){
        const tareas = ref([]);

        provide('tareas', tareas);

        return { tareas }
    }
}
</script>