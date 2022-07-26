<template>
    <BoxTask>
        <div class="columns">
            <div class="column is-7">
                {{ tarefa.descricao || '"Tarefa sem descrição"' }}
            </div>
            <div class="column">
                <CronometroTask :tempo-em-segundos="tarefa.duracaoEmSegundos" />
            </div>
        </div>
  </BoxTask>
</template>

<script lang="ts">
import { defineComponent, PropType } from 'vue'
import CronometroTask from './CronometroTask.vue'
import ITarefa from '../Interfaces/ITarefa';
import BoxTask from './BoxTask.vue';

export default defineComponent({
    name: 'TarefaToDo',
    components: { CronometroTask, BoxTask },
    props: {
        tarefa: { type: Object as PropType<ITarefa>, required: true }

    }
})
</script>

<style scoped>
.box {
    background: #faf0ca
}
</style>