<template>
    <div>
        <section>
            <strong class="display">{{ tempoDecorrido }}</strong>
        </section>
    </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
    name: 'CronometroTask',
    props: {
        tempoEmSegundos: { type: Number, default: 0 }
    },
    computed: {
        tempoDecorrido(): string {
            return new Date(this.tempoEmSegundos * 1000).toISOString().slice(11, -5)
        }
    },
})
</script>

<style scoped>
    .display{
        color: var(--texto-primario)
    }
</style>